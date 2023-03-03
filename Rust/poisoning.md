# Poisoning
* In unsafe code, not all types ensure _maximal_ exception safety. It's possible that code that panics could fail
to correctly update its value, and produce an inconsistent program state.
* Some types are especially good at smuggling values across the panic boundary.
* These types may choose to explicitly _poison_ themselves if they witness a panic.
* Generally poisoning just means preventing normal usage from proceeding.
* The most notable example is standard library's `Mutex`. A Mutex will poison itself if one of its `MutexGuard`s
is dropped during a panic. Any future attempts to lock the `Mutex` will return an `Err` or panic
* The data in such a Mutex was likely in the middle of being modified, and may be in an inconsistent or incomplete state.
* An `RwLock` like `Mutex`, will become poisoned on a panic. However, that an `RwLock` may only be poisoned if a panic occurs while it is locked exclusively (write mode).
If a panic occurs in any reader, then the lock will not be poisoned.

## Reference
[Poisoning - The Rustonomicon](https://doc.rust-lang.org/nomicon/poisoning.html)
