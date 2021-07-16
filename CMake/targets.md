# Targets

Target is to CMake what object is to C++

## Two Main Ways to Add Targets
* `add_executable`
* `add_library`

## PUBLIC, PRIVATE, and INTERFACE
![Keywords example](https://gitee.com/againxx/image-storage/raw/master/images/04-mermaid-libs.svg =750x)

* Only `Interface Library`, `Public Library`, and `Main Library` will affect `myprogram`
* There are two collections of properties
    - **private properties** control what happens when you build that target (`PRIVATE`, `PUBLIC`)
    - **interface properties** tell targets linked to this one what to do when building (`PUBLIC`, `INTERFACE`)

## Pseudo Targets
Don't represent outputs of the buildsystem, but only input such as external dependencies, aliases or other non-build artifacts

### Imported Target
主要用来表示已经存在的shared/static/module/object/executable文件, 一般来说仅在被创建的目录及其子目录可见, 可以通过`GLOBAL`选项设置全局可见

* `add_library(<name> <SHARED|STATIC|MODULE|OBJECT|UNKNOWN> IMPORTED [GLOBAL])`
* `add_executable(<name> IMPORTED [GLOBAL])`

The most important properties are:
* `IMPORTED_LOCATION` which specifies the location of the main library file on disk.
* `IMPORTED_OBJECTS` for object libraries, specifies the location of object files on disk.
* `PUBLIC_HEADER` files to be installed during `install()` invocation

> CMake doesn't allow to install IMPORTED libraries as TARGETS
Reasons:
1. Imported targets were originally designed for importing from an existing installation of some external package so installing didn't make sense at the time
2. When install a *normal* library, CMake is able to modify it for adjust some properties like `RPATH`.
   Such modification is possible because CMake **knows how the library has been built**.
   This is a main advantage of installing library as a `TARGET`.
   But the `IMPORTED` library CMake has no information about the library's compilation process, and cannot perform any reasonable modification of it.

### Interface Target
* Has no `LOCATION` and is mutable, but is otherwise similar to `IMPORTED` target
* 主要用来表示一些概念上的target, 对纯头文件库进行封装, 或者封装一些usage requirement / property
* 只能是library, 不能是executable
* `add_library(<name> INTERFACE [IMPORTED [GLOBAL]])`

#### Interface Imported
需要导入外部的纯头文件库的时候使用INTERFACE IMPORTED target

## Describe the relationship between targets
CMake use `target_link_libraries` and keywords `PUBLIC`, `PRIVATE`, `INTERFACE` to connect targets together

### The importance of head files
> You have a library, `my_lib`, made from `my_lib.hpp` and `my_lib.cpp.` It requires at least C++14 to compile.
> If you then add my_exe, and it needs `my_lib,` should that force `my_exe` to compile with C++14 or better?

1. Whether `my_exe` needs C++14 or not is a build requirement
2. Build requirement often relies on **dependence's header files**
3. If header file `my_lib.hpp` contains C++14 features, this is a **PUBLIC** requirement
4. If header file is valid in all versions of C++, and only the implementations inside `my_lib.cpp` require C++14, then this is a **PRIVATE** requirement
5. If the `my_lib.cpp` does not include the `my_lib.hpp` and does not require C++14, the need of C++14 from `my_lib.hpp` is a **INTERFACE** requirement


## Reference
* [[https://stackoverflow.com/questions/36648375/what-are-the-differences-between-imported-target-and-interface-libraries|imported vs interface]]
* [cmake - Can I install shared imported library? - Stack Overflow](https://stackoverflow.com/questions/41175354/can-i-install-shared-imported-library)
* [Working with Targets – More Modern CMake](https://hsf-training.github.io/hsf-training-cmake-webpage/04-targets/index.html)
* [CMake target_link_libraries Interface Dependencies - Stack Overflow](https://stackoverflow.com/questions/26037954/cmake-target-link-libraries-interface-dependencies)
