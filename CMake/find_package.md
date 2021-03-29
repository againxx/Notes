# find_package

Finds and loads settings from an external project

## Auto set variables
* `<PackageName>_FOUND` is set by cmake
* Other variables or imported targets are set according to individual package documentations

## Basic signature
```cmake
find_package(<PackageName> [version] [EXACT] [QUIET] [MODULE]
             [REQUIRED] [[COMPONENTS] [components...]]
             [OPTIONAL_COMPONENTS components...]
             [NO_POLICY_SCOPE])
```

* `QUIET` disables informational messages (including package cannot be found when it's not `REQUIRED`)
* `[version]` two possible forms
    - a single version `major[.minor[.patch[.tweak]]]`
    - a version range `versionMin...[<]versionMax`, where versionMin/Max have the same format as single version (cmake 3.19 or later)
    - by default, both end points are included, use `<` to exclude upper end point
* `EXACT` requests the version to be matched exactly
* `MODULE` only use module mode to search package
    - If `MODULE` is absent, CMake 

## Two modes for searching package
### Module mode
In module mode, CMake searches for a file named `Find<PackageName>.cmake`
* Firstly, it searches in `CMAKE_MODULE_PATH`
* Then, among Find Modules provided by the CMake installation

#### What's the problem of module mode?
* There is a lot of guessing in `Find<PackageName>.cmake` file. The package authors actually know the usage requirement of their packages
  but the information is completely thrown away when they created the packages
* Therefore, only use a find module for **third party** libraries that do not **support clients to use CMake**

### Config mode
In config mode, CMake searches for a file named `<PackageName>Config.cmake / <lower-case-package-name>-config.cmake`
* A cache entry called `<PackageName>_DIR` is created to hold the directory containing the config file
    - So we can specify a custom `<PackageName>_DIR` for CMake to search
    - If `<PackageName>_DIR` has been set to a directory not containing a config file CMake will ignore it and search from scratch
* The full path to the config file is stored in the cmake variable `<PackageName>_CONFIG`

## Search Procedure
```
<prefix>/                                                       (W)
<prefix>/(cmake|CMake)/                                         (W)
<prefix>/<name>*/                                               (W)
<prefix>/<name>*/(cmake|CMake)/                                 (W)
<prefix>/(lib/<arch>|lib*|share)/cmake/<name>*/                 (U)
<prefix>/(lib/<arch>|lib*|share)/<name>*/                       (U)
<prefix>/(lib/<arch>|lib*|share)/<name>*/(cmake|CMake)/         (U)
<prefix>/<name>*/(lib/<arch>|lib*|share)/cmake/<name>*/         (W/U)
<prefix>/<name>*/(lib/<arch>|lib*|share)/<name>*/               (W/U)
<prefix>/<name>*/(lib/<arch>|lib*|share)/<name>*/(cmake|CMake)/ (W/U)
```

* `W` is the convention installation path in window, `U` is in unix, but all directories are still searched on all platform
