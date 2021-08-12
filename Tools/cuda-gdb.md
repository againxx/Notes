# Cuda-GDB

## Compilation
* Before debugging, compile `.cu` file with `nvcc -g -G` flags, (`-G` generate debug symbol for device code, `-g` has normal meaning)

## Initialization File
* same as `.gdbinit`, read commands from `.cuda-gdbinit`

## Environment Variables
| Variable                              | Usage                                                                               |
|---------------------------------------|-------------------------------------------------------------------------------------|
| CUDA_ENABLE_COREDUMP_ON_EXCEPTION     | generate gpu core dump when exception occurs                                        |
| CUDA_ENABLE_CPU_COREDUMP_ON_EXCEPTION | generate cpu core dump when gpu exception occurs                                    |
| CUDA_DEVICE_WAITS_ON_EXCEPTION        | run normally until a device exception occurs, wait for cuda-gdb to attach to itself |

## Change Focus
* All the cuda-gdb commands apply to the entity in focus (host thread / device thread)
* Debugging cuda programs is just like a cpu program with many threads, although these threads will step simultaneously
* Software coordinates and hardware coordinates
    - **device**, **sm**, **warp**, **lane** are the hardware terminologies for different granularity
    - **kernel**, **block**, **thread** are software terms
* use `cuda device/sm/warp/lane/kernel/block/thread` to check current focus
* use `cuda device 0 sm 1 warp 2 lane 3` to change focus, or `cuda thread (15)` the omitted coordinates will keep current value instead

## Breakpoints & Execution
* Device code single-stepping works at warp level (32 threads have to step altogether) for current focused warp
* `__syncthreads()` will resume all threads and temporarily break them
* Use `__noinline__` keyword to force function to be not inlined
* When a breakpoint is hit by one thread, there is no guarantee that the other threads will hit it at the same time. So the same breakpoint may be hit several times
    - Check current focus to figure out which thread was stopped
* `set cuda break_on_launch application` break on the first instruction of every launched kernel
* Conditional breakpoints can use any builtin variables such as `threadIdx` and `blockIdx` but **not function calls**
    - the process of hitting the conditional breakpoint and evaluate the expression is time-consuming
* Watchepoints on cuda code are **not supported**!

## Inspect states
* `print &array` to check where the variable is stored (register/local/shared/const/global)
* `print array[0]@4` gdb's artificial array syntax is allowed
* Directly examine memory contents, `print *(@shared int*)0x20`
