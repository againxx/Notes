# CMake executable in command line

## 0. Install
去官网下载最新版本的`.sh`文件
`sudo sh cmake.sh --prefix=/usr/local/ --exclude-subdir`

## 1. Generate a project buildsystem

CMake project的关键概念:  
* __Source Tree__: 从包含源文件的最顶层目录开始，以一个顶层CMakeLists.txt为标记
* __Build Tree__: 从包含buildsystem文件和build输出文件（例如：执行文件和库）的最顶层目录开始，以一个CMakeCache.txt文件为标记
* __Generator__: 实际生成的buildsystem（例如：Makefile, VS sln等） 

----------

**命令格式**
commands[^1] | description
:-|:-
`cmake [<options>] <path-to-source>` | path-to-source处为source tree，在当前目录下生成build tree
`cmake [<options>] <path-to-existing-build>` | 使用已经存在的build tree，读取CMakeCache.txt中的路径作为source tree
`cmake [<options>] -S <path-to-source> -B <path-to-build>` | build tree对应的目录可自动生成（如build目录）

[^1]: 方括号代表可选的

----------

**其他参数**  
`-D <var>:<type>=<value>, -D <var>=<value>`  
`-D<var>:<type>=<value>, -D<var>=<value>`空格可省略  
创建或者更新CMake `CACHE`项，`CACHE`项主要用于可定制的设置，type是`set(CACHE)`中能指定的一种  
常用:
* `-DCMAKE_BUILD_TYPE=` `Debug/Release/MinSizeRel/RelWithDebInfo`
* `-DCMAKE_INSTALL_PREFIX=\path\to\install`
* `-DBUILD_SHARED_LIBS=ON` 默认构建shared库

`-G <generator-name>`

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

## 2. Build a project
## 3. Install a project
