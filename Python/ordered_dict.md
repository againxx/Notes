# OrderedDict

## Cues
* What's the OrderedDict? What's the difference between dict?

## Introduction
An **OrderedDict** is a dictionary subclass that remembers the order that keys were first inserted

```python
from collections import OrderedDict 

print("This is a Dict:\n") 
d = {} 
d['a'] = 1
d['b'] = 2
d['c'] = 3
d['d'] = 4

for key, value in d.items(): 
    print(key, value) 
    
# ('a', 1)
# ('c', 3)
# ('b', 2)
# ('d', 4)

print("\nThis is an Ordered Dict:\n") 
od = OrderedDict() 
od['a'] = 1
od['b'] = 2
od['c'] = 3
od['d'] = 4

for key, value in od.items(): 
    print(key, value) 

# ('a', 1)
# ('b', 2)
# ('c', 3)
# ('d', 4)

```

## Dicts are now ordered
> Changed in version 3.7: Dictionary order is guaranteed to be insertion order. This behavior was an implementation detail of CPython from 3.6.
