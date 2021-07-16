# GCC

## Options for Linking
* `-l<library>` when searching, shared libraries have preference unless the `-static` option is set
    - the linker searches and processes libraries and object files in the order they are specified
    - so the libraries with symbol definitions should come **last**

## Options That Control Optimization
* `-fif-conversion` attempt to transform conditional jumps into branch-less equivalents (e.g. conditional moves)
* `-fomit-frame-pointer` don't keep the frame pointer in a register (RBX) for functions that don't need one
    - this can make RBX be used as general purpose register and spare the room for optimizations
    - but make the debugger harder for back tracing (don't know where the stack frames begin and end)
* `-ffunction-sections / -fdata-sections` place each function or data item into its own section in the output file

## Options for Code Generation Conventions
* `-fcommon` whether to put uninitialized global variables into COMMON block, the default is `-fno-common` (put them in .bss section)
    - this behavior is inconsistent with C++ and may have speed and code size penalty

## Options for Developers
* `-fdump-class-hierarchy` output a representation of each class's hierarchy and virtual function table layout to a file `<source>.class`

## Precompiled Headers
* `gcc xxx.h` compile header files will generate a precompiled headers that accelerate following compilations

## Reference
[c - Trying to understand gcc option -fomit-frame-pointer - Stack Overflow](https://stackoverflow.com/questions/14666665/trying-to-understand-gcc-option-fomit-frame-pointer)
