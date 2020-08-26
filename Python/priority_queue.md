# PriorityQueue
The `queue.PriorityQueue` uses the same `heapq` implementation internally. However, different in
* it is **synchronized** so supports concurrent processes
* it is a `class` interface compared to the `function` based interface of `heapq`

## Example
```python
from queue import PriorityQueue

# we initialise the PQ class instead of using a function to operate upon a list. 
customers = PriorityQueue()
customers.put((2, "Harry"))
customers.put((3, "Charles"))
customers.put((1, "Riya"))
customers.put((4, "Stacy"))

while not customers.empty():
     print(customers.get()) # Will print names in the order: Riya, Harry, Charles, Stacy.
```
