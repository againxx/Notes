# Attrs

```python
import attr

# auto_attribs: use type annotation instead of attr.ib() to declare attributes
# cmp: disable > >= < <=
# frozen: make the class immutable
@attr.s(auto_attribs=True, cmp=False, frozen=True)
class Point:
    x: float
    y: float
    z: float

    def __iter__(self):
        yield from (self.x, self.y, self.z)

    def __eq__(self, other):
        if not isinstance(other, Point):
            return NotImplemented
        return tuple(self) == tuple(other)

    def __hash__(self):
        return hash(tuple(self))
```

## Reference
* [Easier Classes: Python Classes Without All The Cruft - YouTube](https://www.youtube.com/watch?v=vD1KZgHCNCs)
