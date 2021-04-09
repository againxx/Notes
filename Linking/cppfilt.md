# c++filt

A tool can demangle C++ names

* `readelf -Ws <elf_file> | c++tilt`, don't forget the `-W` option of `readelf` otherwise the demangled name will be truncated
