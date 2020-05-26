# String Formatting
## Overview
There are three ways in Python for string formatting:
1. %-formatting
2. str.format()
3. f-strings (after python3.6)

[Complete Version](https://realpython.com/python-f-strings/)

## %-formatting
```python
first_name = "Eric"
last_name = "Idle"
age = 74
profession = "comedian"
affiliation = "Monty Python"
print("Hello, %s %s. You are %s. You are a %s. You were a member of %s." \
      % (first_name, last_name, age, profession, affiliation))
# Hello, Eric Idle. You are 74. You are a comedian. You were a member of Monty Python.
```
Cons:
* verbose and leads to errors, like not displaying tuples or dictionaries correctly.
* become less readable once you start using long string.

## str.format()

```python
first_name = "Eric"
last_name = "Idle"
age = 74
profession = "comedian"
affiliation = "Monty Python"
print(("Hello, {first_name} {last_name}. You are {age}. " + 
       "You are a {profession}. You were a member of {affiliation}.") \
       .format(first_name=first_name, last_name=last_name, age=age, \
               profession=profession, affiliation=affiliation))
# Hello, Eric Idle. You are 74. You are a comedian. You were a member of Monty Python.
```
You can also use ** to do this neat trick with dictionaries:
```python
person = {'name': 'Eric', 'age': 74}
print("Hello, {name}. You are {age}.".format(**person))
# Hello, Eric. You are 74.
```
Pros:
* much more easily readable than code using %-formatting

Cons:
* still be quite verbose when you are dealing with multiple parameters and longer strings.

## f-strings

### Simple Syntax
Similar to str.format() but less verbose, also valid to use a capital F
```python
name = "Eric"
age = 74
print(f"Hello, {name}. You are {age}.")
print(F"Hello, {name}. You are {age}.")
# Hello, Eric. You are 74.
```
### Arbitrary Expression
f-strings are evaluated at runtime, you can put any and all valid Python expressions in them.
```python
name = "Eric Idle"
print(f"{to_lowercase(name)} is funny.")
print(f"{name.lower()} is funny.")
# eric idle is funny.
```

You could even use objects created from classes with f-strings.  
[the str() and repr() method](https://realpython.com/operator-function-overloading/) deal with how objects are presented as strings.  
By default, f-strings will use \_\_str__(), but you can make sure they use \_\_repr__() if you include the conversion flag !r.
```python
class Comedian:
def __init__(self, first_name, last_name, age):
    self.first_name = first_name
    self.last_name = last_name
    self.age = age

def __str__(self):
    return f"{self.first_name} {self.last_name} is {self.age}."

def __repr__(self):
    return f"{self.first_name} {self.last_name} is {self.age}. Surprise!"

new_comedian = Comedian("Eric", "Idle", "74")
print(f"{new_comedian}")
# Eric Idle is 74.
f"{new_comedian!r}"
# Eric Idle is 74. Surprise!
```
If you want to spread strings over multiple lines, you also have the option of escaping a return with a \\:
```python
name = "Eric"
profession = "comedian"
affiliation = "Monty Python"
message = f"Hi {name}. " \
          f"You are a {profession}. " \
          f"You were in {affiliation}."

print(message)
# Hi Eric. You are a comedian. You were in Monty Python.
```
### Format Output
```python
total = 10_100_000_000
print(f'{total:,}')
```
