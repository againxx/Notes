# Atomic Flag

Atomics guarantee two characteristics:
* They are atomic
* They provide synchronization and order constraints on the program execution

## Properties
* The only guaranteed lock-free atomic
* The building block for higher thread abstractions

## Interface
* `clear` method set its value to `false`
* `test_and_set` set back to `true` and return the old value
* `std::atomic_flag` must be initialized to `false` with the constant `ATOMIC_FLAG_INIT`
