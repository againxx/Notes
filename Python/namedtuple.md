# Namedtuple

## Cues
* What's different between namedtuple and dict?
* How do I construct a namedtuple object?
* How many ways can I use to access the elements of the namedtuple?
* How do I convert a dict to a namedtuple?
* How do I convert a namedtuple to an OrderedDict?
* How do I construct a namedtuple from an iterable object?
* How do I show all keynames of a namedtuple?
* How do I change the value of a given key of a namedtuple?
* Do I know there are two different ways to use namedtuples?
* What are drawbacks to using namedtuples?

## Basic
* Present in module `collections` / `typing`
* Like dictionaries they contain keys that are hashed to a particular value.
But on contrary, it supports both access from key value and **iteration**, the functionality that dictionaries lack.
Besides, it can save some typing than dictionary if you use the same structure multiple times.
* It's often used when a class only has a few properties but no method (like structure in C++)

## Access Operations
There are three ways to access namedtuple's elements
* index
* keyname
* getattr()
```python
# importing "collections" for namedtuple()
import collections
from typing import NamedTuple

# Declaring namedtuple()
Student = collections.namedtuple('Student', ['name', 'age', 'DOB'])

# With default values
fields = ("age", "eye_color", "hair_color")
Profile = collections.namedtuple("Profile", fields, defaults=(18, "brown", "blue")

# Type hint for namedtuple, equivalent to the above declaration
class Student(NamedTuple):
    name: str
    age: int
    DOB: str

# Adding values
S = Student('Nandini', 19, '2541997')

# Access using index
print("The Student age using index is: ", end="")
print(S[1])

# Access using name
print("The Student name using keyname is: ", end="")
print(S.name) # Cannot be accessed by S['name']

# Access using getattr()
print("The Student DOB using getattr() is: ", end="")
print(getattr(S, 'DOB'))
```

## Conversion Operations
* `_make()`: return a `namedtuple` instance from the `iterable`
* `_asdict()`: return an `OrderedDict` instance from the mapped value of `namedtuple`
* `**` operator: convert a `dict` into a `namedtuple`

```python
# initializing iterable
li = ['Manjeet', 19, '411997']

# initializing dict
di = {'name': "Nikhil", 'age': 19 , 'DOB': '1391997'}

# using _make() to return namedtuple()
print("The namedtuple instance using iterable is: ")
print(Student._make(li))
# same as using unpacking from iterable
print(Student(*li))

# using _asdict() to return an OrderedDict()
print("The OrderedDict instance using namedtuple is: ")
print(S._asdict())

# using ** operator to return namedtuple from dictionary
print("The namedtuple instance from dict is: ")
print(Student(**di))
```

## Additional Operations
* `_fields()`: return all the keynames of the namespace declared
* `_replace()`: change the values mapped with the passed keyname

```python
# using _fields to display all the key names of namedtuple()
print("All the fields of students are: ")
print(S._fields)

# using _replace() to change the attribute values of namedtuple
# return a new namedtuple, don't change original one
print("The modified namedtuple is: ")
print(S._replace(name='againxx'))

# AttributeError: can't set attribute
S.name = 'againxx'
```

## Performance
* namedtuple的实例消耗的内存和tuple一样, 因为字段名都被存放在对应的类里
* 这个实例甚至比普通对象实例要小一些, 因为Python不用`__dict__`来存放这些实例的属性

## Implicitly Generated Methods
* `__repr__`
* `__eq__` `__ne__` `__lt__` `__gt__` `__le__` `__ge__`
* `__add__` `__mul__`
* `__len__`

## Problems
* `NamedTuple` is inherited from `tuple`
    - Consequently, it comes with many undesirable dunder method

## Reference
[geeksforgeeks - namedtuple in python](https://www.geeksforgeeks.org/namedtuple-in-python/)
