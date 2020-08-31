# Targets

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

### Interface Target
* Has no `LOCATION` and is mutable, but is otherwise similar to `IMPORTED` target
* 主要用来表示一些概念上的target, 对纯头文件库进行封装, 或者封装一些usage requirement
* 只能是library, 不能是executable
* `add_library(<name> INTERFACE [IMPORTED [GLOBAL]])`

#### Interface Imported
需要导入外部的纯头文件库的时候使用INTERFACE IMPORTED target

[[https://stackoverflow.com/questions/36648375/what-are-the-differences-between-imported-target-and-interface-libraries|imported vs interface]]
