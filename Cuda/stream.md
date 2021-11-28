# Stream

Stream is a way for task parallelism in CUDA

* A stream is a sequence of commands (possibly issued by different host threads) that execute in order
* Different streams, may execute their commands out of order with respect to one another or concurrently, therefore inter-kernel communication if undefined
* The commands issued on a stream may execute when all the dependencies of the command are met, which includes
    - previously launched commands on same stream
    - or dependencies from other streams
* Kernel launches and host `<->` device memory copies that do not specify any stream parameter, or set the stream parameter to zero, are issued to the default stream. They are therefore **executed in order**
* `CUDA_API_PER_THREAD_DEFAULT_STREAM` macro before including CUDA headers (`cuda.h` and `cuda_runtime.h`) will let each host thread has its own default stream

## Stream Synchronization
### Explicit
* `cudaDeviceSynchronize()` waits until all preceding commands in **all** streams of all host threads have completed
* `cudaStreamSynchronize(stream_id)` waits until all preceding commands in the given stream have completed
* `cudaStreamWaitEvent(stream_id, event)` makes all the commands added to the given stream after the call to `cudaStreamWaitEvent` delay their execution until the given event has completed
* `cudaStreamQuery()` provides applications with a way to know if all preceding commands in a stream have completed

### Implicit
