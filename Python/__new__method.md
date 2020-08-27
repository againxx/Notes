# __new__ method

Whenever a class is instantiated, `__new__` and `__init__` methods are called
* `__new__` method will be called when an object is created
* `__init__` method will be called to initialize the object

```python
class class_name:
    def __new__(cls, *args, **kwargs):
        # some statements
        return super(class_name, cls).__new__(cls, *args, **kwargs)
        # or
        return object.__new__(cls, *args, **kwargs)
```

* `__new__` method is executed first and decides whether to use __init__ method or not
* `__init__` method is called every time an instance of the class is returned by `__new__`,
  passing the instance to the `__init__` as the `self` parameter
* `__init__`'s purpose is just to alter the fresh state of the newly created instance, and cannot return anything
* if `super` is omitted for `__new__` method, the `__init__` method won't be executed

```python
class A(object): 
    def __new__(cls): 
        print("Creating instance") 

    # It is not called 
    def __init__(self): 
        print("Init is called") 

print(A()) 
# Creating instance
# None
```

* `__new__` method can return an instance of a different class
```python
# class whose object 
# is returned 
class GeeksforGeeks(object): 
    def __str__(self): 
        return "GeeksforGeeks"
        
# class returning object 
# of different class 
class Geek(object): 
    def __new__(cls): 
        return GeeksforGeeks() 
        
    def __init__(self): 
        print("Inside init") 
        
print(Geek()) # GeeksforGeeks
```

## Reference
[__new__ in Python - GeeksforGeeks](https://www.geeksforgeeks.org/__new__-in-python/)
