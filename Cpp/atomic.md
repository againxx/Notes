# Atomic

## What's the difference between compare_exchange_strong and compare_exchange_weak?
* `compare_exchange_strong(old_x, new_x)` means `if (x == old_x) { x = new_x; return true; } else { old_x = x; return false;}`
* `compare_exchange_weak` means the same thing but can **spuriously fail**
* Conceptually, the `compare_exchange_strong` is implemented as following, here Lock is not a real mutex but some form of exclusive access implemented in hardware
```cpp
bool compare_exchange_strong(T& old_v, T new_v) {
    T tmp = value;  // Current value of atomic
    if (tmp != old_v) {
        old_v = tmp;
        return false;
    }
    Lock l;  // Get exclusive acceses
    tmp = value;  // value could have changed!
    if (tmp != old_v) {
        old_v = tmp;
        return false;
    }
    value = new_v;
    return true;
}

// If exclusive access is hard to get, than we have compare_exchange_weak
bool compare_exchange_weak(T& old_v, T new_v) {
    T tmp = value;  // Current value of atomic
    if (tmp != old_v) {
        old_v = tmp;
        return false;
    }
    TimedLock l;  // Get exclusive acceses or fail
    if (!l.locked()) return false;  // old_v is correct
    tmp = value;  // value could have changed!
    if (tmp != old_v) {
        old_v = tmp;
        return false;
    }
    value = new_v;
    return true;
}
```

## Lock-Free Algorithm
* The key point of lock-free algorithm is to use atomic variables as gateways to memory access (as a generalized pointer)
* Atomics can be used to get exclusive access to non-atomic memory or to reveal memory to other threads
* To achieve this, atomic has an other side - memory barrier
    - Memory barriers control how changes to memory made by one thread become visible to other threads
    - Memory barriers are invoked through processor-specific instructions
    - Memory barriers are often "attributes" on read/write operations, ensuring the specified order of reads and writes

## Memory Order/Barrier
### Acquire Barrier
* Acquire barrier guarantees that all memory operations scheduled after the barrier in the program order become visible after the barrier
    - "All operations" include both reads and writes
    - "All operations" not just operations on the same variable that the barrier was on
* Reads and writes cannot be reordered from after to before the barrier

### Release Barrier
* Release barrier guarantees that all memory operations scheduled before the barrier in the program order become visible before the barrier
- Reads and writes cannot be reordered from before to after the barrier

* The common usage for acquire-release pair:
    - Thread 1 prepares data (done some writes) then **releases** (publishes) it by update atomic variable x
    - Thread 2 **acquires** atomic variable x and the data is guaranteed to be visible

### Sequential Consistency Order
* Removes that requirement on single atomic variable and establishes single total modification order of atomic variables
