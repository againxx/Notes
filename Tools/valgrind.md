# Valgrind

```shell
valgrind [valgrind-options] your-prog [your-prog-options]
```

使用memcheck工具的常用流程
1. `cmake -DCMAKE_BUILD_TYPE=Debug ..` 也可考虑加上`-O1`
2. `valgrind --log-file=<log_file> prog` 大致查看错误数量
3. `valgrind --num-callers=<number> --log-file=<log_file> prog` 若错误的调用栈过多, 可增加num-callers的大小
4. `valgrind --gen-suppressions=all --log-file=<log_file> prog` 若有错误需要suppression,
注意`--gen-suppressions=yes`需要确认每一条错误, 不适合结合log-file使用
5. `valgrind --gen-suppressions=all --suppressions=<supp_file> --log-file=<log_file> prog` 添加并修改suppression, 不断缩小错误范围

## 编译要求
* `-g` include exact line numbers
* `-O1` balance between speed and accuracy
* `-O0` slow
* `-O2` and above is not recommended as Memcheck occasionally reports uninitialised-value errors which don’t really exist.
* `-fno-inline` 不对函数进行inline展开, 使得函数调用链看起来更清晰

## 工具集
Valgrind分为两部分, core和tools, 各有各自的参数.
当代码第一次执行执行时, core将代码交给所选择的tool, tool添加上自己的指令, 并将代码返回给core.
* memcheck (default)
* cachegrind (cache and branch-prediction profiler)
* callgrind (call-graph generating cache profiler)
    - 可以显示编译后的程序一共有多少条指令
* kcachegrind 可视化callgrind和cachegrind的输出文件

## Options
### Core
| Option                            | Description                                                                        |
|-----------------------------------|------------------------------------------------------------------------------------|
| `--tool=<tool_name>`                | 选择工具                                                                           |
| `--log-fd=<file_descriptor>`        | 将结果输出到文件描述符, 默认是2(stderr)                                            |
| `--log-file=<file_name>`            | 将结果输出到文件                                                                   |
| `--read-inline-info=yes`            | 读取内联函数信息, 同样能让函数调用链更清晰, 即使编译时有内联                       |
| `-v`                                | 详细输出                                                                           |
| `-v -v`                             | 更详细的输出                                                                       |
| `--gen-suppressions=<no/yes/all>`   | 为每一条error输出相应的suppression格式, yes需要用户确认, all则输出所有suppressions |
| `--default-suppressions=no`         | 不使用默认的suppressions                                                           |
| `--suppressions=/path/to/file.supp` | 使用指定的suppression文件, 可指定多次                                              |
| `--num-callers=<number>`            | 设置stack traces中显示的最大数量, 默认是12                                         |

### Memcheck
| Option                             | Description                                       |
|------------------------------------|---------------------------------------------------|
| `--leak-check=<no/summary/yes/full>` | 默认为summary, 设置为full/yes会将每个泄露单独列出 |
| `--track-origins=yes`                | 默认为no, 控制是否追踪uninitialised values的来源  |

## Suppression
1. First line: a name in the summary of used suppressions
2. Second line: name of the tool(s) (if more than one, comma-separated), and the name of suppression itself, separated by colon
e.g. `tool_name1,tool_name2:suppression_name`
3. Next line: a small number of suppression types have extra information after the second line
4. Remaining lines: calling context for the error -- chain of function calls that led to it.
    - Locations may be names of either shared objects or functions. They begin `obj:` and `fun:` respectively.
    - Function and object names to match against may use the wildcard characters `*` and `?`.
    - Frame-level wildcard `...` matches zero or more frames.
5. Finally, the entire suppression must be between curly braces. Each brace must be the first character on its own line.

### Some Examples
```
{
__gconv_transform_ascii_internal/__mbrtowc/mbtowc
Memcheck:Value4
fun:__gconv_transform_ascii_internal
fun:__mbr*toc
fun:mbtowc
}
```

```
{
libX11.so.6.2/libX11.so.6.2/libXaw.so.7.0
Memcheck:Value4
obj:/usr/X11R6/lib/libX11.so.6.2
obj:/usr/X11R6/lib/libX11.so.6.2
obj:/usr/X11R6/lib/libXaw.so.7.0
}
```

```
{
a-contrived-example
Memcheck:Leak
fun:malloc
...
fun:ddd
...
fun:ccc
...
fun:main
}
```

## 常见错误 (memcheck)
* Invalid read / Invalid write
* Conditional jump or move depends on uninitialized value(s)
* Syscall param write(buf) points to uninitialised byte(s) / Syscall param exit(error_code) contains uninitialised byte(s)
* Invalid free()
* Mismatched free() / delete / delete []
* Source and destination overlap in memcpy
* Argument ’size’ of function malloc has a fishy (possibly negative) value

## Cooperate with GDB
* `--vgdb=<no/yes/full>` valgrind will provide a "gdbserver" when `yes/full` is specified
    - `vgdb` is a valgrind version "gdb" command line tool, which can send monitor commands to the valgrind when no gdb is being used
* `--vgdb-error=<number>` freeze the program after number errors
* `--vgdb-stop-at=<set>` freeze the program for other events
