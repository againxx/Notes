# Toolchains

* A toolchain is used by CMake to drive the build process, such as compiling, linking libraries and creating archives.
* In normal builds, CMake automatically determines the toolchain for host builds based on configured languages and system defaults.
* In cross-compiling, a toolchain file may be specified with information about compiler and utility paths.
