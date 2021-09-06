# Dictionary View Object

Instead of creating a `list` / sequence from `dict.keys()`, python returns a **Dict View Object**

Methods that return dict view objects:
1. `dict.keys()`, which should inherit from `collections.abc.KeysView`
2. `dict.values()`, which should inherit from `collections.abc.ValuesView`
3. `dict.items()`, which should inherit from `collections.abc.ItemsView`

## Properties
* The returned objects will reflect the original dict's change dynamically
* It supports the following operations
    - `len(dictview)` returns the length of original dict
    - `iter(dictview)` returns an iterator over the keys, values or items
        - `keys()` and `values()` all keep the same insertion order, so they can be combined with `zip(values(), keys())` to get (value, key) pairs
    - `x in dictview` can be used to check the ownership of keys, values or items
    - `reversed(dictview)` support reversely iteration (since Python 3.8)
* Keys views are **set-like** and support many set operations, if all values are _hashable_ then items view is also **set-like**
