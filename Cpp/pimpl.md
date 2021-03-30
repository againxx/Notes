# PImpl

"Pointer to implementation" or "pImpl" is a C++ programming technique that
removes implementation details of a class from its object representation by placing them in a separate class, accessed through an opaque pointer:

## Advantages
* Optimize compilation times
    - Changes in implementation do not require components that only depend on interface to be recompiled
* Completely hide the implementation when distributing a pre-compiled library
    - Pimpl can hide private member declarations as well, otherwise, you need to include them in public header files
* Switch class implementations transparently to user of the class
