# Super Function

`super()` alone returns a temporary object of the superclass that allows you to call that superclass's methods

Advantages:
* Saves you from needing to rewrite those methods in your subclass
* Allows you to swap out superclasses with minimal code changes

## An Example
```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * self.length + 2 * self.width

class Square(Rectangle):
    def __init__(self, length):
        super().__init__(length, length)

class Cube(Square):
    def surface_area(self):
        face_area = super().area()
        return face_area * 6

    def volume(self):
        face_area = super().area()
        return face_area * self.length
```

**Notice**: `Cube` class doesn't have an `__init__()`. You can skip defining it,
and the `__init__()` of the superclass (`Square`) will be called automatically.

## A super() Deep Dive
`super()` can also take two parameters
1. the first parameter is the subclass type
2. the second parameter is an object that is an instance of that subclass
3. the second parameter can also be a type, in which case `issubclass(type2, type2)` must be true (this is useful for classmethods)

### The First Parameter
```python
# In Python3, the super(Square, self) call is
# equivalent to the parameterless super() call
class Square(Rectangle):
    def __init__(self, length):
        super(Square, self).__init__(length, length)

class Cube(Square):
    def surface_area(self):
        face_area = super(Square, self).area()
        return face_area * 6
```

By setting Square as the subclass argument to `super()` instead of Cube, you can let `super()` to
start searching for a matching method (in this case, `area()`) at one level above Square in the
instance hierarchy, in this case Rectangle.

In this specific example, the behavior doesn’t change. But imagine that Square also implemented
an `area()` function that you wanted to make sure Cube did not use. Calling `super()` in this way allows you to do that.

> **Caution**: The parameterless call to `super()` is recommended and sufficient for most use cases,
> and needing to change the search hierarchy regularly could be indicative of a larger design issue.

### The Second Parameter
By including an instantiated object, `super()` returns a bound method: a method that is bound to the object,
which gives the method the object’s context such as any instance attributes. If this parameter is not included,
the method returned is just a function, unassociated with an object’s context.

> **Note**: Technically, `super()` doesn’t return a method. It returns a **proxy** **object**.
> This is an object that delegates calls to the correct class methods without
> making an additional object in order to do so.

## Reference
[Supercharge Your Classes With Python super()](https://realpython.com/python-super/#super-in-multiple-inheritance)
