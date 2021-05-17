# GCC

## Options for Linking
* `-l<library>` when searching, shared libraries have preference unless the `-static` option is set
    - the linker searches and processes libraries and object files in the order they are specified
    - so the libraries with symbol definitions should come **last**

## Options That Control Optimization
* `-fif-conversion` attempt to transform conditional jumps into branch-less equivalents (e.g. conditional moves)

## Options for Code Generation Conventions
* `-fcommon` whether to put uninitialized global variables into COMMON block, the default is `-fno-common` (put them in .bss section)
    - this behavior is inconsistent with C++ and may have speed and code size penalty

## Options for Developers
* `-fdump-class-hierarchy` output a representation of each class's hierarchy and virtual function table layout to a file `<source>.class`
