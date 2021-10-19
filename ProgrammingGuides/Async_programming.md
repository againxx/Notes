# Async Programming

## Three main excution models
* Single-threaded synchronous
* Multiple-threaded synchronous
* Single-threaded asynchronous

## Problems with multi-thread
* The spawned threads may still interleave in a single thread, since thread management is controlled by OS
* Threads need to coordinate and communicate with each other
* Thread switching has extra cost

## Asynchronous model
* Only one task will be executing at any given time
