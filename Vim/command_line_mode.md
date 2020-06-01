# Command Line Mode

**Ex命令影响范围广且距离远**

## 命令行窗口快捷键
* `<C-b>` go to the beginning of the command
* `<C-e>` go to the end of the command
* `<C-d>`可列出当前可用的补全(目前设置下和`<Tab>`等同)
* `<C-r><C-w>`把当前光标下的word插入命令行
* `<C-r><C-a>`把当前光标下的WORD插入命令行
* `@:` 重复上次的Ex命令, 运行过一次之后可再用`@@`重复

## 命令行窗口
* use `q:` in normal mode to open the editable buffer for all history commands(command-line window)
* use `q/` to open search history window
* `<C-f>` in command line mode has the same effect as `q:`, useful in `<C-r>=`
* in command-line window
    - use `<Enter>` to execute the command
    - use `<C-c>`(I remap it to `<C-c><C-x>`) to continue in command line mode
    - use `:q` to discard the command line and go back to normal mode

## 操作缓冲区文本的Ex命令
| Commands                    | Usage                                          |
|-----------------------------|------------------------------------------------|
| :[range]d[elete] [x]        | 删除指定范围内的行[到寄存器x中]                |
| :[range]y[ank] [x]          | 复制指定范围的行[到寄存器x中]                  |
| :[line]pu[t] [x]            | 在指定行后粘贴寄存器x中的内容                  |
| :[range]co[py] {address}    | 把指定范围内的行拷贝到{address}所指定的行之下  |
| :t                          | synonym for copy                               |
| :[range]m[ove] {address}    | 把指定范围内的行移动到{address}所指定的行之下  |
| :[range]j[oin]              | 连接指定范围的行                               |
| :[range]norm[al] {commands} | 对指定范围内的每一行执行普通模式命令{commands} |
| :r[ead] [name]              | 插入文件name(默认是当前文件)的内容到当前光标下 |
| :[range]r[ead] !{cmd}       | 执行cmd并将标准输出插入到光标下, 或指定行      |

## 其他Ex命令
| Commands               | Usage                                                        |
|------------------------|--------------------------------------------------------------|
| :[range]up[date]       | like ":w", but only write when the buffer has been modified. |
| :!{cmd}                | 在shell中执行{cmd}                                           |
| :[range]w[rite] !{cmd} | 在shell中执行{cmd}, 以[range]作为其标准输入                  |
| :[range]!{filter}      | 使用外部程序{filter}过滤指定的[range]                        |
| :earlier <num>m        | 回退操作历史, num分钟前                                      |
| :later <num>m          | 前进操作历史, num分钟后                                      |
