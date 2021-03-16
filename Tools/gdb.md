# GDB

## Running
* `run <args>` run a program with arguments
* `file <executable>` 读入一个可执行文件

## Information
* `info source` 查看当前活动的source file, 直接指定行号时影响的文件
* `info b[reakpoints]` 查看所有断点

## Breakpoints
* `b <function>`
* `b <line_number>`
* `b <file_name>:<line_number>`
* `b <file_name>:<function>`
* `b +offset / -offset` 当前栈帧中正在执行的源代码前后设置断点
* `b *address` 在虚拟内存地址处设置断点
* `d <breakpoint_num>` delete breakpoint, the number is showed by `info b`

## Step
* `next` c/cpp程序中的下一行(step over)
* `nexti` 汇编中的下一条指令
* `step` step into
* `stepi` step into function call at assembly level

## Disassemble
* `disass[emble]` 反汇编
* `set disassembly-flavor intel` 使用Intel语法(默认是AT&T语法)

## Print
* `p` print variable
* `x/<fmt> <address>` examine memory at address
* `info reg` show values of registers

