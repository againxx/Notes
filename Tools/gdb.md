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
* `disable breakpoints` disable all breakpoints

### Hardware breakpoints
利用x86架构的debug registers, 从而可以让程序全速执行; 否则每执行一条指令时都需要检查表达式的值, 效率极低
* `watch <expression>` 当表达式的值发生变化时, 停止执行
* `watch -l/-location <expression>` 当表达式的值对应的内存地址处的值发生变化时, 停止执行
* `watch <expression> thread 3` watch on specific thread
* `watch foo if foo > 10` conditional watch

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
* `until [location]` Execute until past the current line or past a `location`

## Disassemble
* `disass[emble]` 反汇编
* `set disassembly-flavor intel` 使用Intel语法(默认是AT&T语法)

## Print
* `p <var>` print variable only once, which has the form `$num = value` this `num` can be further referenced as value history
* `display <var>` print the value of a variable at every step
* `undisplay <display_num>` the number is shown by `info display`
* `printf "<format>", <var>` 用C printf函数的格式显示变量的值(only once)
* `x/<fmt> <address>` examine memory at address
* `info reg` show values of registers
* `info variables` show addresses and symbol names for all global and static variables
* `info locals` show names and values of all local variables of current stack frame
* `info args` show names and values of all arguments of current stack frame (function arguments)
* `info symbol <address>` describe what symbol is at location address, only for global or static symbols
* `p &<symbol_name>` print the address of the symbol
* `$n` history value of number n
* `$` lastest value
* `$$[n]` n value before lastest value
* `show values` print last ten values in value history
* `show values n` print ten values centered at history item number n
* `show values +` print ten values just after the values last printed

## Assignment
* `print x=4` set x to 4 and print the result
* `set x=4` only set x to 4 and do not change the value history
* `set variable x=4` set has many subcommannd, prefer `set variable` to avoid conflicts
* `set {int}0x83040 = 4` store values into arbitrary memory location

## Stack back trace
* `backtrace` display the call stack of current function, current function is at top
* `f` fast show where I am
* `f[rame] [level] <frame_num>` select stack frame with level n, frame 0 is the innermost (currently executing) frame
* `f address <stack_address>` select stack frame with stack address
    - check the address using `info frame`
* `f function <function_name>` select the stack frame for function function-name
    - If there are multiple stack frames for function function-name then the inner most stack frame is selected.
* `f view <stack_address> [pc_addr]` view a frame that is not part of GDB's backtrace giving a optional _program counter address_
    - This is useful mainly if the chaining of stack frames is damaged by a bug, making it impossible for GDB to assign stack numbers
* `up [num]` move num frame up the stack toward outermost frame (if num is positive)
* `down [num]` num defaults to 1
* `sel[ect] frame` same as frame without print information

## Process Information
* `info proc` check the process id (PID) of debugged executable
* `info proc mappings` check virtual memory layout
* `cat /proc/<PID>/maps` check virtual memory layout of the given process
* `maintenance info sections` can examine elf file sections information and their corresponding loading address
* `info proc cwd`

## Symbol Information
* `info sharedlibrary` list currently loaded shared libraries
* `info functions` list all known function symbols
* `add-symbol-file <elf_file>` load extra symbols from the given file

## Attach to Running Process
* `gdb -p <PID> <program>`

In recent Linux kernel, if you try to attach debugger to a running process, even if by the same user,
gdb will politely refuse with error message:
> ptrace: Operation not permitted.

The reason is a newly enabled security feature YAMA to specifically restrict inspecting memory of other programs.

* To enable once, as root `echo 0 > /proc/sys/kernel/yama/ptrace_scope`
* To enable permanently, `echo kernel.yama.ptrace_scope = 0 > /etc/sysctl.d/10-ptrace.conf`

## Scripting
* `shell <command>` to run shell command
* `python <command>` to run python command

## Signals
* gdb will capture the debugged program's signals and decide want to do
* `info signals` check the gdb handlers for different signals
* `handle <signals_num> [no]stop [no]print [no]pass` change the signal handler behaviors
* `SIGINT & SIGTRAP` are special, which are used for stop and breakpoint, and will not be passed into the debugged program
    - gdb can add a trap-related instruction to set breakpoints

## Thread
* `info threads`
* `thread apply <thread_num> <command>`
* `thread apply all <command>`

## Reverse Debug
* `record` begin the recording of following instructions
* `set exec direction reverse/forward` make `next` into `reverse-next`
* `show/set record insn-number-max` controls the limit (default 200000) for how many instructions gdb will store
* `show/set record stop-at-limit <on/off>` linear-mode / circular-mode when the buffer is full
* `info record insn-number` show how many instructions are currently saved

## Reference
* [ProcessRecord/Tutorial - GDB Wiki](https://sourceware.org/gdb/wiki/ProcessRecord/Tutorial)
