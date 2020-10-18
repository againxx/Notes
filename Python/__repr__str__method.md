# __repr__ & __str__

## __repr__
* Invoked when we call `repr()` function, which represents a object with a string
* Mainly used by:
    - Interactive console
    - Debugger
    - `%r` in % string format
* It's goal is to be unambiguous
* Implement `__repr__` for any class you implement
* It's a principle that you should make `eval(repr(foo)) == foo`, but it's often an unattainable goal

## __str__
* Invoked when we call `str()` function, which coerces a object to a string
* Mainly used by:
    - `print()`
    - terminal application
* When a object has no `__str__`, interpreter will call `__repr__` instead
* It's goal is to be readable
* Container's `__str__` uses contained objects' `__repr__`
    - The contained objects' `__str__` output may disturb your representation (include "," / ":")
* Implementing `__str__` is optinal

## Reference
[python - Difference between __str__ and __repr__? - Stack Overflow](https://stackoverflow.com/questions/1436703/difference-between-str-and-repr)
