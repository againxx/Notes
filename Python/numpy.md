# Numpy

## dtype=object
[more info](https://stackoverflow.com/questions/29877508/what-does-dtype-object-mean-while-creating-a-numpy-array)

NumPy arrays usually have a single datatype (e.g. integers, floats or fixed-length strings) and then 
the bits in memory are interpreted as values with that datatype.

When creating an array with dtype=object, the memory taken by the array now is filled with pointers to Python objects 
which are being stored elsewhere in memory (much like a Python list is really just a list of pointers to objects, not the objects themselves).

Arithmetic operators such as * don't work with arrays which have a string_ datatype. 
NumPy is just treating the bits in memory as characters and the * operator doesn't make sense here.

```python
np.array(['avinash','jay'], dtype=object) * 2
```

works because now is an array of (pointers to) Python strings. The * operator is well defined for these Python string objects. 
New Python strings are created in memory and a new object array with references to the new strings is returned.

