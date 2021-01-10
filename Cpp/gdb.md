# GDB

## Step
* `next` c/cpp程序中的下一行(step over)
* `nexti` 汇编中的下一条指令
* `step` step into
* `stepi` step into function call at assembly level

## Breakpoint
* `b <line_num>` set breakpoint at line number in current file
* `info b` show breakpoints
* `d <num>` delete breakpoint, the number is showed by `info b`

## Disassemble
* `disass[emble]` 反汇编
* `set disassembly-flavor intel` 使用Intel语法(默认是AT&T语法)

## Print
* `p` print variable
* `x/<fmt> <address>` examine memory at address
* `info reg` show values of registers
