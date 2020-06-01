# Class Variable & Class Method & Static Method

## Class Method
```python
class C:
    @classmethod
    def fun(cls, arg1, arg2, ...):
        ...
```

* A class method is a method which is bound to the class and not the object of the class
* They have the access to the state of the class as it takes a class parameter (cls)
* It can modify a class state that would across all the instances of the class (class variable)

## Static Method
```python
class C:
    @staticmethod
    def fun(arg1, arg2, ...):
        ...
```

* A static method is also a method which is bound to the class and not the object of the class
* A static method can't access or modify class state
* It is present in a class because it makes sense for the method to be present in class

## Class Method vs Static Method
* A class method takes cls as first parameter while a static method doesn't
* A class method can access or modify class state while a static method can't
* We can use class method to create factory methods - factory methods return class object (similar to a constructor)
for different use cases

## Example
Now, python doesn't support method overloading like C++ so we use class methods to create factory methods.

```python
from datetime import date

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # a class method to create a Person object by birth year
    @classmethod
    def from_birth_year(cls, name, year):
        return cls(name, date.today().year - year)

    # a static method to check if a Person is adult or not
    @staticmethod
    def is_adult(age):
        return age > 18

person1 = Person('again', 21)
person2 = Person.from_birth_year('again', 1996)

print Person.is_adult(22)
```
