# Type Hints

## Advantages
1. Easier to reason about code
2. Easier refactoring
3. Easier to use libraries
4. Type linters (mypy)
5. Runtime data validation (pydantic)

## Not Designed for
1. No runtime type inference (解释器运行时不会推导类型, 或者验证传入的参数)
2. No performance tuning (对程序的性能没有影响)

## Type of What
1. Function Arguments
2. Function Return Values
3. Variables

## Four Ways to Add

### Type Annotations

```python
from typing import List
class A(object):
    def __init__() -> None:
        self.elements: List[int] = []

    def add(element: int) -> None:
        self.elements.append(element)
```

### Type Comments

```python
from typing import List
class A(object):
    def __init__():
        # type: () -> None
        self.elements = [] # type: List[int]

    def add(elements):
        # type: (List[int]) -> None
        self.elements.append(element)
```

### Interface Stub Files

Add another file with `pyi` extension -- inference file like C++

```python
# a.pyi alongside a.py
from typing import List
class A(object):
    elements = ... # type: List[int]
    def __init__() -> None: ...
```

### Docstrings

The legacy way

## What to Add

### Nominal Type

Nominal Type are types that have a name to it within the Python Interpreter.
```python
t: Tuple[int, float] = 0, 1.2
d: Dict[str, int] = {"a": 1, "b": 2}
d: MutableMapping[str, int] = {"a": 1, "b": 2}
l: List[int] = [1, 2, 3]
i: Iterable[Text] = [u'1', u'2', u'3']
```

Alias for compound type
```python
OptFList = Optional[List[float]]
```

Elevate builtin type, which can be useful to avoid errors where for example
you pass in two arguments with the same type in the wrong order to a function:
```python
UserId = NewType('UserId', int)
user_id = UserId(524313)
count = 1
call_with_user_id_n_times(user_id, count)
```

For `namedtuple` you can attach your type information directly
```python
class Employee(NamedTuple):
    name: str
    id: int
```

Composing type of _one of_ and _optional of_
```python
Union[None, int, str] # one of
Optional[float] # either float or None
```

Type hint callback function
```python
# syntax is Callback[[Arg1Type, Arg2Type], ReturnType]
def feeder(get_next_item: Callback[[], str]) -> None:
```

One can define it's own generic containers by using the `TypeVar` construction
```python
T = TypeVar('T')
class Magic(Generic[T]):
    def __init__(self, value: T) -> None:
        self.value: T = value

def square_values(vars: Iterable[Magic[int]]) -> None:
    v.value = v.value * v.value
```

Disable type checking wherever it's not needed by using the `Any` type hint
```python
def foo(item: Any) -> int:
    item.bar()
```
