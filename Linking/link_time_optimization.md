# Link Time Optimization

## Why we need link time optimization?
* When functions are all in the same transition unit, the compiler can perform efficient interprocedural optimization
* However, this optimization will break if we separate functions into several files
* Therefore, the linking stage becomes the feasible time to perform these optimizations again

## Problems that obstruct optimization
* Aliasing problem in function parameters
