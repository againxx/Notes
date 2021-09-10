# Context Manager


## Single use / Reusable / Reentrant
### Single use
* Single use context manager can only be used effectively in a **with** statement **once**, and must be created afresh each time they're used
* Attempting to use them a second time will trigger and exception or not work correctly
* Examples include: file managers, `contextmanager()`

### Reentrant
* Reentrant context mananger can not only be used in multiple **with** statements
* But may also be used inside a **with** statement that is already using the same context manager (nested context manager)

```python
from contextlib import redirect_stdout
from io import StringIO
stream = StringIO()
write_to_stream = redirect_stdout(stream)
with write_to_stream:
    print("This is written to the stream rather than stdout")
    with write_to_stream:
        print("This is also written to the stream")

print("This is written directly to stdout")
print(stream.getvalue())
```

### Reusable
* Reusable context managers support being used multiple times
* But will fail (or work incorrectly) if the specific context manager instance has already been used in a containing **with** statement

```python
from contextlib import ExitStack
stack = ExitStack()
with stack:
    stack.callback(print, "Callback: from first context")
    print("Leaving first context")

with stack:
    stack.callback(print, "Callback: from second context")
    print("Leaving second context")

with stack:
    stack.callback(print, "Callback: from outer context")
    with stack:
        stack.callback(print, "Callback: from inner context")
        print("Leaving inner context")
    print("Leaving outer context")
# Leaving inner context
# Callback: from inner context
# Callback: from outer context
# Leaving outer context
# not nestable
```
