# Constant Memory

* Constant memory is a special-purpose memory used for data that is read-only and accessed uniformly by threads in a warp
* While constant memory is read-only from kernel codes, it is both readable and writable from the host
* Constant memory resides in device DRAM and has a **dedicated** on-chip cache
* There is a 64KB limit on the size of constant memory cache per SM
* Constant memory's best access pattern is if all threads in a warp access the same location in constant memory
    - Accesses to different addresses by threads within a warp are serialized
* Constant variables must be declared in **global** scope with `__constant__` qualifier
* Because the device is only able to read constant memory, values in constant memory must be initialized from host code using `cudaMemcpyToSymbol`
* Constant memory variables can be visible across multiple source files when using the CUDA separate compilation capability

## Read-Only Cache
* Kepler GPUs add the ability to use the GPU texture pipeline as a read-only cache for data stored in global memory
* This is a **seprate** read-only cache with separate memory bandwidth from normal global memory reads, use of this feature can yield a performance benefit for bandwidth-limited kernels
* There is a total of 48 KB of read-only cache per Kepler SM
* Generally, the read-only cache is better for scattered reads than the L1 cache, and **should not** be used when threads in a warp all read the same address
* There are two ways to indicate to the compiler that data is read-only for the duration of kernel
     - Using an intrinsic function `__ldg`
     - Qualifying pointers to global memory with `const __restrict__`

```cuda
// intrinsic way
__global__ void kernel(float* output, float* input) {
    output[idx] += __ldg(&input[idx]);
}

// qualifying way
__global__ void kernel(float* output, const float* __restrict__ input) {
    output[idx] += input[idx];
}
```

### Compare with constant memory
* The read-only cache is seprate and distinct from the constant cache
* Data loaded through the constant cache must be relatively small and must be accessed uniformly for good performance
    - all threads of a warp should access the same location at any given time
* Whereas, data loaded through the read-only cache can be much larger and can be accessed in a non-uniform pattern

## Summary
* Both constant cache and read-only cache are read-only from the device.
* Both have limited per-SM resources: The constant cache is 64KB, and the read-only cache is 48 KB.
* Constant cache performs better on uniform reads (where every thread in a warp accesses the same address).
* Read-only cache is better for scattered reads.
