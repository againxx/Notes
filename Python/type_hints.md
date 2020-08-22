# Type Hints

## Advantages - 优点
1. Easier to reason about code
2. Easier refactoring
3. Easier to use libraries
4. Type linters (mypy)
5. Runtime data validation (pydantic)

## Not Designed for - 不适用
1. No runtime type inference (解释器运行时不会推导类型, 或者验证传入的参数)
2. No performance tuning (对程序的性能没有影响)

## Type of What - 添加于
1. Function Arguments
2. Function Return Values
3. Variables

## Four Ways to Add - 四种添加的方式

### Type Annotations (python 3.6+)
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

### Nominal Type - 命名类型

The convention is to import types using the form `from typing import Iterable` 
(as opposed to `import typing` or `import typing as t` or `from typing import *`)

**Nominal Type** are types that have a name to it within the Python Interpreter.
```python
t1: Tuple[int, float] = 0, 1.2
t2: Tuple[int, ...] = 0, 1, 2, 3 # use ... to specify a variable-length tuple
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

# This is equivalent to
Employee = collections.namedtuple('Employee', ['name', 'id'])
```

Composing type of _one of_ and _optional of_
```python
Union[None, int, str] # one of
Optional[float] # either float or None
```

Annotate a callable (function) value
```python
def f(num1: int, my_float: float = 3.5) -> float:
    return num1 + my_float

x: Callable[[int, float], float] = f
```

A generator function that yields ints is secretly just a function that returns an iterator of ints
```python
def g(n: int) -> Iterator[int]:
    i = 0
    while i < n:
        yield i
        i += 1
```

Type hint callback function
```python
# syntax is Callback[[Arg1Type, Arg2Type], ReturnType]
def feeder(get_next_item: Callback[[], str]) -> None:
```

One can define it's own generic containers by using the `TypeVar` construction, `TypeVar` is like template T in C++, 
the class inherits from `Generic[T]` is like template class in C++
```python
T = TypeVar('T')
class Magic(Generic[T]): # Template class
    def __init__(self, value: T) -> None:
        self.value: T = value

def square_values(vars: Iterable[Magic[int]]) -> None:
    for v in vars:
        v.value = v.value * v.value
```

An argument can be declared position-only by giving it a name starting with two underscores
```python
def quux(__x: int) -> None:
    pass

quux(2) # fine
quux(__x=3) # error
```

Function overloads, when you have functions of Union parameters or Union returns, 
you can use overloads decorator to help type checker understand.
```python
from typing import Optional, overload

@overload
def get_foo(foo_id: None) -> None:
    pass

@overload
def get_foo(foo_id: int) -> int:
    pass

def get_foo(foo_id: Optional[int]) -> Optional[Foo]:
    if foo_id is None:
        return None
    return Foo(foo_id)

reveal_type(get_foo(None)) # None
reveal_type(get_foo(1))    # Foo
```
To find out what type mypy infers for an expression anywhere in your program, wrap it in `reveal_type()`.  
Mypy will print an error message with the type; remove it again before running the code

### Duck Type - 鸭子类型
Duck theorem: if it quacks like a duck, and acts like a duck, then most definitely for all intended purposes it is a duck.

#### Standard Duck Type
```python
from typing import Mapping, MutableMapping, Sequence, Iterable, List, Set

# Use Iterable for generic iterables (anything usable in "for"),
# and Sequence where a sequence (supporting "len" and "__getitem__") is
# required
def f(ints: Iterable[int]) -> List[str]:
    return [str(x) for x in ints]

f(range(1, 3))

# Mapping describes a dict-like object (with "__getitem__") that we won't
# mutate, and MutableMapping one (with "__setitem__") that we might
def f(my_mapping: Mapping[int, str]) -> List[int]:
    my_mapping[5] = 'maybe'  # if we try this, mypy will throw an error...
    return list(my_mapping.keys())

f({3: 'yes', 4: 'no'})

def f(my_mapping: MutableMapping[int, str]) -> Set[str]:
    my_mapping[5] = 'maybe'  # ...but mypy is OK with this.
    return set(my_mapping.values())

f({3: 'yes', 4: 'no'})
```

#### Custom Duck Type
```python
from typing_extensions import Protocol

class Renderable(Protocol):
    def render(self) -> str: ...

def render(obj: Renderable) -> str:
    return obj.render()

class Foo:
    def render(self) -> str:
        return "Foo!"

render(Foo()) # Clean!
render(3) # Error: expected Renderable
```

### Escape Hatch - 抑制错误警告
#### Any
Disable type checking wherever it's not needed by using the `Any` type hint
```python
def foo(item: Any) -> int:
    item.bar()
```

#### cast
Tell type checker the type in some special cases by using `cast`. It's only for mypy -- there's no runtime check.
```python
from typing import cast
my_confit = get_config_attr("my_config")
reveal_type(my_config) # Any

my_config = cast(
    Dict[str, int],
    get_config_attr("my_config"),
)
reveal_type(my_config) # Dict[str, int]
```

#### ignore
Reserve this one for bugs in the type checker, or some other limitations we can't not work around
```python
# github.com/python/mypy/issues/1362
@property # type: ignore
@timer
def is_visible(self) -> bool:
    ...
```

## Questions
### What is the difference between TypeVar and NewType?
> TypeVar let you refer to the same type more than once without specifying exactly which type it is.

Use type `Action` in both parameter and return value
```python
Action = TypeVar('Action')

def action(self, action: Action) -> Action:
    pass
```

> A NewType is for when you want to declare a distinct type without actually doing the work of creating a new type
> or worry about the overhead of creating new class instances.

[Stack overflow answer](https://stackoverflow.com/questions/58755948/what-is-the-difference-between-typevar-and-newtype)
