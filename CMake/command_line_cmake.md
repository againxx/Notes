# CMake executable in command line

## 0. Install
去官网下载最新版本的`.sh`文件  
`sudo sh cmake.sh --prefix=/usr/local/ --exclude-subdir`

## 1. Generate a project buildsystem

CMake project的关键概念:  
* __Source Tree__: 从包含源文件的最顶层目录开始，以一个顶层CMakeLists.txt为标记
* __Build Tree__: 从包含buildsystem文件和build输出文件（例如：执行文件和库）的最顶层目录开始，以一个CMakeCache.txt文件为标记
* __Generator__: 实际生成的buildsystem（例如：Makefile, VS sln等）


### 命令格式
| commands[^1]                                               | description                                                         |
|:-----------------------------------------------------------|:--------------------------------------------------------------------|
| `cmake [<options>] <path-to-source>`                       | path-to-source处为source tree，在当前目录下生成build tree           |
| `cmake [<options>] <path-to-existing-build>`               | 使用已经存在的build tree，读取CMakeCache.txt中的路径作为source tree |
| `cmake [<options>] -S <path-to-source> -B <path-to-build>` | build tree对应的目录可自动生成（如build目录）                       |

[^1]: 方括号代表可选的

### 其他参数
`-D <var>:<type>=<value>, -D <var>=<value>`  
`-D<var>:<type>=<value>, -D<var>=<value>`空格可省略  
创建或者更新CMake `CACHE`项，`CACHE`项主要用于可定制的设置，type是`set(CACHE)`中能指定的一种  
常用:
* `-DCMAKE_BUILD_TYPE=Debug/Release/MinSizeRel/RelWithDebInfo`
* `-DCMAKE_INSTALL_PREFIX=/path/to/install`
* `-DBUILD_SHARED_LIBS=ON` 默认构建shared库

`-G <generator-name>`

`-P <cmake-script-file>` run a script

`--system-information` output the default compilers and the corresponding options

**不同CMAKE_BUILD_TYPE的区别**

CMAKE_BUILD_TYPE影响:
1. Optimization (level) [`-O0, -O1, -O2, -O3, -Ofast, -Os, -Oz, -Og, -O, -O4`]
2. Including 'debug info' in the executable [`-g, -gline-tables-only, -gmodules, -glevel, -gcoff, -gdwarf, -gdwarf-version, -ggdb, -grecord-gcc-switches, -gno-record-gcc-switches, -gstabs, -gstabs+, -gstrict-dwarf, -gno-strict-dwarf, -gcolumn-info, -gno-column-info, -gvms, -gxcoff, -gxcoff+, -gz[=type]`]
3. Generating code for `assert()` or not [`-DNDEBUG`]
4. Including debug (output) code or not [custom]

不同CMAKE_BUILD_TYPE的默认编译选项:
1. Release: `-O3 -DNDEBUG`
2. Debug: `-g`
3. RelWithDebInfo: `-O2 -g -DNDEBUG`
4. MinSizeRel: `-Os -DNDEBUG`

For buildsystem that support multi-type configuration, use `CMAKE_CONFIGURATION_TYPES` to set multiple types
* `cmake .. -G"Visual Studio 12 2017 Win64" -D CMAKE_CONFIGURATION_TYPES="Release;Debug"`
* `cmake --build . --config Release` use `--config` to decide build which configuration

## 2. Build a project

构建一个已经生成的binary tree  
`cmake --build <dir> [<options>] [-- <build-tool-options>]`
| options                            | description                                                                                 |
|------------------------------------|---------------------------------------------------------------------------------------------|
| `--build <dir>`                    | binary tree directory                                                                       |
| `--parallel [<jobs>], -j [<jobs>]` | 指定最大并行进程数, 省略的话使用原生build工具的默认值                                       |
| `--target <tgt>..., -t <tgt>...`   | 构建tgt而不是默认的target, 可以指定多个空格分割的target, 可以通过help来查看生成了哪些target |
| `--clean-first`                    | 先build clean target然后再build                                                             |
| `--verbose, -v`                    | 开启详细输出, 包括具体的build commands                                                      |
| `--`                               | 将剩余的参数传给原生build工具, 也可以用`-- VERBOSE=1`来开启详细输出                         |

## 3. Install a project
`cmake --install <dir> [<options>]`
| Options             | Description                 |
|---------------------|-----------------------------|
| `--install <dir>`   | binary tree directory       |
| `--prefix <prefix>` | overide installation prefix |
| `-v, --verbose`     | enable verbose output       |

## 4. Cross compiling
`cmake -DCMAKE_TOOLCHAIN_FILE=path/to/file` will load a toolchain file to set values for compilers

## 5. Reference
[Complete Version](https://cmake.org/cmake/help/latest/manual/cmake.1.html)
