# Cuda Architectures

New in version 3.18

* We can now use target property `CUDA_ARCHITECTURES` to control cuda device code generation
* There is also a global version `CMAKE_CUDA_ARCHITECTURES` to initialize new targets' property
* An architecture can be suffixed by either `-real` or `-virtual` to specify the kind of architecture to generate code for.
  If no suffix is given then code is generated for both real and virtual architectures.
* This property is equivalent to private one, therefore cannot be propagated to other targets

## Examples
* Generates code for real and virtual architectures 30, 50 and 72.
`set_property(TARGET tgt PROPERTY CUDA_ARCHITECTURES 35 50 72)`

* Generates code for real architecture 70 and virtual architecture 72.
`set_property(TARGET tgt PROPERTY CUDA_ARCHITECTURES 70-real 72-virtual)
`
* CMake will not pass any architecture flags to the compiler.
`set_property(TARGET tgt PROPERTY CUDA_ARCHITECTURES OFF)`
