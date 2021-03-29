# GDB

## Running
* `run <args>` run a program with arguments
* `start <args>` run a program with arguments and stop at main()
* `file <executable>` 读入一个可执行文件

## Information
* `info source` 查看当前活跃的source file, 直接指定行号时影响的文件
* `i[nfo] b[reakpoints]` 查看所有断点
* `i[nfo] display` 查看所有display点

## Breakpoints
* `b <function>`
* `b <line_number>`
* `b <file_name>:<line_number>`
* `b <file_name>:<function>`
* `b +offset / -offset` 当前栈帧中正在执行的源代码前后设置断点
* `b *address` 在虚拟内存地址处设置断点
* `d <breakpoint_num>` delete breakpoint, the number is showed by `info b`, 不提供number的话则删除所有的断点
* `enable <breakpoint_num>`
* `disable <breakpoint_num>`

### Hardware breakpoints
利用x86架构的debug registers, 从而可以让程序全速执行; 否则每执行一条指令时都需要检查表达式的值, 效率极低
* `watch <expression>` 当表达式的值发生变化时, 停止执行
* `watch -l/-location <expression>` 当表达式的值对应的内存地址处的值发生变化时, 停止执行

```cpp
int a = 1;
int b = 2;
int c = 1;
int *p = &a;
// watch *p
p = &c; // not break
p = &b; // break

// watch -l p
p = &c; // break
p = &b; // break
```

* `rwatch <expression>` 当表达式的值被读取时, 停止执行
* `rwatch -l/-location <expression>` 当表达式的值对应的内存地址处的值被读取时, 停止执行

## Step
* `next` c/cpp程序中的下一行(step over)
* `nexti` 汇编中的下一条指令
* `step` step into
* `stepi` step into function call at assembly level
* `finish` exit current function and return to the caller function

## Disassemble
* `disass[emble]` 反汇编
* `set disassembly-flavor intel` 使用Intel语法(默认是AT&T语法)

## Print
* `p <var>` print variable only once
* `display <var>` print the value of a variable at every step
* `undisplay <display_num>` the number is shown by `info display`
* `printf "<format>", <var>` 用C printf函数的格式显示变量的值(only once)
* `x/<fmt> <address>` examine memory at address
* `info reg` show values of registers

## Stack back trace
* `backtrace` display the call stack of current function, current function is at top
* `f[rame] [level] <frame_num>` select stack frame with level n, frame 0 is the innermost (currently executing) frame
* `f address <stack_address>` select stack frame with stack address
    - check the address using `info frame`
* `f fucntion <function_name>` select the stack frame for function function-name
    - If there are multiple stack frames for function function-name then the inner most stack frame is selected.
* `f view <stack_address> [pc_addr]` view a frame that is not part of GDB's backtrace giving a optional _program counter address_
    - This is useful mainly if the chaining of stack frames is damaged by a bug, making it impossible for GDB to assign stack numbers
* `up [num]` move num frame up the stack toward outermost frame (if num is positive)
* `down [num]` num defaults to 1
