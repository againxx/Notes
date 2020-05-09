# Command Line Mode

**Ex命令影响范围广且距离远**

* use `q:` in normal mode to open the editable buffer for all history commands(command-line window)
* `<C-f>` in command line mode has the same effect as `q:`, useful in `<C-r>=`
* in command-line window
    - use `<Enter>` to execute the command
    - use `<C-c>`(I remap it to `<C-c><C-x>`) to continue in command line mode
    - use `:q` to discard the command line and go back to normal mode
* `<C-b>` go to the beginning of the command
* `<C-e>` go to the end of the command
* `:read` 可以将命令的输出写入buffer

## 操作缓冲区文本的Ex命令
| Commands                    | Usage                                          |
| :[range]d[elete] [x]        | 删除指定范围内的行[到寄存器x中]                |
| :[range]y[ank] [x]          | 复制指定范围的行[到寄存器x中]                  |
| :[line]pu[t] [x]            | 在指定行后粘贴寄存器x中的内容                  |
| :[range]co[py] {address}    | 把指定范围内的行拷贝到{address}所指定的行之下  |
| :t                          | synonym for copy                               |
| :[range]m[ove] {address}    | 把指定范围内的行移动到{address}所指定的行之下  |
| :[range]j[oin]              | 连接指定范围的行                               |
| :[range]norm[al] {commands} | 对指定范围内的每一行执行普通模式命令{commands} |
