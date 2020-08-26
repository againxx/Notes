# Heapq
> An implementation of min binary heap

A binary heap is a binary tree with two properties:
* It’s a **complete tree** (All levels are completely filled except possibly the last level and the last level has all keys as left as possible).
  This property of Binary Heap makes them suitable to be stored in an **array**.
* A binary heap is either **Min Heap** or **Max Heap**. In a Min Binary Heap, the key at root must be minimum among all keys present in Binary Heap.
  The same property must be recursively true for all nodes in Binary Tree.

## Operations
* heapify(iterable)
* heappush(heap, element)
* heappop(heap)
* heappushpop(heap, element)
* heapreplace(heap, element)
* nlargest(k, iterable, key=fun)
    - **key**, if provided, specifies a function of one argument that is used to extract a comparison key from each element in iterable
* nsmallest(k, iterable, key=fun)

## Examples
```python
import heapq

li = [5, 7, 9, 1, 3]

# using heapify to convert list into heap
heapq.heapify(li)
print(li) # [1, 3, 9, 7, 5]

heapq.heappush(li, 4)
print(li) # [1, 3, 4, 7, 5, 9]

print(heapq.heappop(li)) # 1
print(li) # [3, 5, 4, 7, 9]
```

```python
li1 = [5, 7, 9, 4, 3]
li2 = [5, 7, 9, 4, 3]

heapq.heapify(li1)
heapq.heapify(li2)

# using heappushpop() to push and pop items simultaneously, first push then pop
print(heapq.heappushpop(li1, 2)) # pops 2

# using heapreplace() to push and pop items simultaneously, first pop then push
print(heapq.heapreplace(li2, 2)) # pops 3
```

```python
li1 = [6, 7, 9, 4, 3, 5, 8, 10, 1]

# using nlargest to print 3 largest numbers
print(heapq.nlargest(3, li1)) # prints 10, 9 and 8

# using nsmallest to print 3 smallest numbers
print(heapq.nsmallest(3, li1)) # prints 1, 3 and 4
```

## Reference
* [Heap queue (or heapq) in Python - GeeksforGeeks](https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/)
* [Introduction to Binary Heaps (MaxHeaps) - YouTube](https://www.youtube.com/watch?v=WCm3TqScBM8)
