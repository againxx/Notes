# Namedtuple

Present in module `collections`

Like dictionaries they contain keys that are hashed to a particular value.
But on contrary, it supports both access from key value and iteration, the functionality that dictionaries lack.

[Original Version](https://www.geeksforgeeks.org/namedtuple-in-python/)

## Access Operations
There are three ways to access namedtuple's elements
* index
* keyname
* getattr()
```python
# importing "collections" for namedtuple() 
import collections 

# Declaring namedtuple() 
Student = collections.namedtuple('Student', ['name', 'age', 'DOB']) 

# Adding values 
S = Student('Nandini', 19, '2541997') 

# Access using index 
print ("The Student age using index is : ", end ="") 
print (S[1]) 

# Access using name 
print ("The Student name using keyname is : ", end ="") 
print (S.name) # Cannot be accessed by S['name']

# Access using getattr() 
print ("The Student DOB using getattr() is : ", end ="") 
print (getattr(S, 'DOB')) 
```

## Conversion Operations
* `_make()`: return a `namedtuple` instance from the `iterable`
* `_asdict()`: return an `OrdereDict` instance from the mapped value of `namedtuple`
* `**` operator: convert a `dict` into a `namedtuple`

```python
# initializing iterable 
li = ['Manjeet', 19, '411997' ] 

# initializing dict 
di = { 'name' : "Nikhil", 'age' : 19 , 'DOB' : '1391997' } 

# using _make() to return namedtuple() 
print ("The namedtuple instance using iterable is : ") 
print (Student._make(li)) 

# using _asdict() to return an OrderedDict() 
print ("The OrderedDict instance using namedtuple is : ") 
print (S._asdict()) 

# using ** operator to return namedtuple from dictionary 
print ("The namedtuple instance from dict is : ") 
print (Student(**di)) 
```

## Additional Operations
* `_fields()`: return all the keynames of the namespace declared
* `_replace()`: change the values mapped with the passed keyname

```python
# using _fields to display all the keynames of namedtuple() 
print ("All the fields of students are : ") 
print (S._fields) 

# using _replace() to change the attribute values of namedtuple 
# return a new namedtuple, don't change original one
print ("The modified namedtuple is : ") 
print(S._replace(name = 'againxx'))

# AttributeError: can't set attribute
S.name = 'againxx'
```
