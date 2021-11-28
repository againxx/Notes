# GPU Compilation

## GPU Generations
* Binary compatibility is not guaranteed across different generations
    - instruction set and instruction encodings may change
* Binary compatibility within one GPU generation can be guaranteed under certain conditions because they share the basic instruction set
* In the CUDA naming scheme, GPUs are named `sm_xy`, where `x` denotes the GPU generation number, and `y` the version in that generation

## Two Stage Compilation
* Unlike CPU applications, `nvcc` relies on a **two stage** compilation model for ensuring application compatibility with future GPU generations
     - A `nvcc` compilation command always uses two architectures: a _virtual_ intermediate architecture, plus a _real_ GPU architecture to specify the intended processor to execute on.
     - The _real_ architecture must be an **implementation** of the _virtual_ architecture
* GPU compilation is performed via an intermediate representation - PTX, which can be considered as assembly for a virtual GPU architecture
* A virtual GPU architecture provides only a (largely) generic instruction set, but not binary instruction encoding (PTX programs are always represented in text format)
    - The chosen virtual architecture is more of a statement on the GPU capabilities that the application requires
    - Using a _smallest_ virtual architecture still allows a _widest_ range of actual architectures for the second `nvcc` stage
    - Virtual architecture should always be chosen as **low** as possible, thereby maximizing the actual GPUs to run on.
    - Real architecture should be chosen as **high** as possible (assuming that this always generates better code)

![virtual & real architectures](https://gitee.com/againxx/image-storage/raw/master/images/20211127101041.png =750x)

## Further Mechanisms
Compilation staging in itself does not help towards the goal of application compatibility with future GPUs, there are two other mechanisms
    - Just in time compilation (JIT)
    - Fatbinaries

### JIT
* By specifying a virtual code architecture instead of a real GPU, `nvcc` postpones the assembly of PTX code until application runtime
* The command below allows generation of exactly matching GPU binary code, when the application is launched on an `sm_50` or later architecture
    - `nvcc x.cu --gpu-architecture=compute_50 --gpu-code=compute_50`

![just-in-time compilation](https://gitee.com/againxx/image-storage/raw/master/images/20211127103125.png =750x)

### Fatbinaries
* A different solution to overcome startup delay by JIT while still allowing execution on newer GPUs is to specify multiple code instances
    - `nvcc x.cu --gpu-architecture=comptue_50, --gpu-code=compute_50,sm_50,sm_52`

### NVCC options
* `--gpu-architecture (-arch)` specify virtual architecture
    - when `--gpu-code` is not specified, can also specify real architecture, the `--gpu-code` values default to the _closest_ virtual architecture,
    plus the `--gpu-architecture` value itself
    - if `--gpu-architecture` is a virtual architecture and `--gpu-code` is empty, it is also used as effective `--gpu-code` value
* `--gpu-code (-code)` specify real architectures
    - when `--gpu-code` has virtual architecture, the stage 2 translation will be omitted for such virtual architecture, and the stage 1 PTX result will be embedded instead

Examples:
```
nvcc x.cu --gpu-architecture=sm_52
nvcc x.cu --gpu-architecture=compute_50
```
are equivalent to
```
nvcc x.cu --gpu-architecture=compute_52, --gpu-code=compute_52,sm_52
nvcc x.cu --gpu-architecture=compute_50, --gpu-code=compute_50
```

* The combination of `--gpu-architecture` and `--gpu-code` can be used in all cases where code is to be generated for one or more GPUs using a common virtual architecture,
which means the program will not conditionally choose features to use
* Sometimes the device code can use conditional compilation based on the value of architecture identification macro `__CUDA_ARCH__`
* In this case, it's possible using `--generate-code (-gencode)` with sub-options `arch` and `code`
* Unlike `--gpu-architecture`, `--generate-code` may be repeated on the command line

For example, the following assumes absence of half-precision floating-point operation support for the `sm_50` and `sm_52` code, but full support on `sm_53`
```
nvcc x.cu \
    --generate-code arch=compute_50,code=[sm_50,sm_52] \
    --generate-code arch=compute_53,code=sm_53
```

### Macros
* The `__CUDA_ARCH__` macro is assigned a three-digit value string `xy0` during each `nvcc` compilation stage 1 that compiles for `compute_xy`
* The architecture list macro `__CUDA_ARCH_LIST__` is a list of comma-separated `__CUDA_ARCH__` values for each of the virtual architectures specified in the compiler invocation
