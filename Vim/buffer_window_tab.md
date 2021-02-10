# Buffer & Window & Tab

## Buffer
Buffer即内存中待编辑的文件，例`vim .vimrc .zshrc`会同时打开两个buffer
| 操作Buffer      | Description                                                                                  |
|:----------------|:---------------------------------------------------------------------------------------------|
| `:ls, :buffers` | 列出所有的buffer                                                                             |
| `:bd[elete]`    | 关闭当前的buffer                                                                             |
| `:bn[ext]`      | 切换到下个buffer                                                                             |
| `:wn[ext]`      | write current file and start editing the next file                                           |
| `:bp[revious]`  | 切换到上个buffer                                                                             |
| `:bf[irst]`     | 切换到第一个buffer                                                                           |
| `:bl[ast]`      | 切换到最后一个buffer                                                                         |
| `:b<N>`         | 切换到第N个buffer，`:ls`可以显示buffer的index                                                |
| `:b {bufname}`  | 切换到可以由{bufname}标示的缓冲区, {bufname}只需包含文件路径中足以唯一标识此缓冲区的字符即可 |
| `bufdo`         | 在`:ls`列出的所有缓冲区上执行Ex命令                                                          |
| `Ctrl-^`        | 切换到最近编辑的buffer，可以用于两个文件之间轮流切换                                         |

## Window
* Window是可视化buffer的一个视点，即将屏幕分窗
* 将同一个buffer显示在两个window的作用, 修改长文件时可以参考文件不同部位的内容

| 操作Window                     | Description                                      |
|:-------------------------------|:-------------------------------------------------|
| `:sp[lit] <file>, Ctrl-w + s`  | 水平分割窗口, 或在新窗口打开文件                 |
| `:vs[plit] <file>, Ctrl-w + v` | 垂直分割窗口, 或在新窗口打开文件                 |
| `:new, Ctrl-w + n`             | 创建一个水平分割窗口, 并在其中编辑空文件         |
| `:vne[w]`                      | 创建一个垂直分割窗口, 并在其中编辑空文件         |
| `CTRL-w + hjkl`                | 在不同窗口间移动, 自定义为`ALT-hjkl`             |
| `Ctrl-w + p`                   | 移动到之前的窗口, 自定义为`ALT-p`                |
| `Ctrl-w + w`                   | 移动到下方或者右方的窗口                         |
| `Ctrl-w + W`                   | 移动到上方或者左方的窗口                         |
| `:q[uit], Ctrl-w + q`          | 关闭当前窗口                                     |
| `:c[lose], Ctrl-w + c`         | 关闭当前窗口，只剩最后一个窗口时不会关闭         |
| `:on[ly], Ctrl-w + o`          | 仅保留当前窗口                                   |
| `Ctrl-w + r`                   | 调整窗口的位置, 循环调整                         |
| `Ctrl-w + R`                   | 调整窗口的位置, 反向循环调整                     |
| `Ctrl-w + x`                   | 交换当前窗口和下一个窗口                         |
| `Ctrl-w + HJKL`                | 调整窗口的位置, 指定上下左右                     |
| `Ctrl-w + hjkl`                | 在上下左右分割窗口, 并将光标置于对应窗口(自定义) |
| `Ctrl-w + T`                   | 将当前窗口移动到一个新标签页                     |
| `Ctrl-w + _`                   | 垂直方向最大化当前窗口                           |
| `<N>Ctrl-w + _`                | 把当前活动窗口的高度设为N行                      |
| `Ctrl-w + <bar>`               | 水平方向最大化当前窗口                           |
| `<N>Ctrl-w + <bar>`            | 把当前活动窗口的宽度设为N列                      |
| `Ctrl-w + =`                   | 使各窗口均等                                     |
| `Ctrl-w + <>`                  | 左右调整窗口大小, 自定义为`ALT-,.`               |
| `Ctrl-w + +-`                  | 上下调整窗口大小, 自定义为`ALT-=-`               |
| `lcd <path>`                   | 设置当前窗口的本地工作目录                       |
| `Ctrl-w + ]`                   | 在水平分割窗口中打开tag所在文件                  |
| `Ctrl-w + f`                   | 在水平分割窗口中打开光标下的文件                 |
| `Ctrl-w + F`                   | 在水平分割窗口中打开光标下的文件, 并跳转到指定行 |

## Tab (layout)
Tab是用来配置不同Window布局的
| 操作Tab                                       | Description                                         |
|:----------------------------------------------|:----------------------------------------------------|
| `:tabnew [file_path], :tabe[dit] [file_path]` | 打开空的新标签或者在新标签里打开文件                |
| `gt, :tabn[ext]`                              | 切换到下个标签                                      |
| `gT, :tabp[revious]`                          | 切换到上一个标签                                    |
| `<N>gt`                                       | 切换到第N个标签                                     |
| `:tabc[lose]`                                 | 关闭当前标签                                        |
| `:tabo[nly]`                                  | 仅保留当前标签                                      |
| `:tabm[ove] [N]`                              | 重排标签页, 当N为0时, 移动到开头, 省略N时移动到末尾 |
| `:windo lcd <path>`                           | 为当前标签页的所有窗口设置本地工作目录              |
| `Ctrl-w + gf`                                 | 在新tab中打开光标下的文件                           |
| `Ctrl-w + gF`                                 | 在新tab中打开光标下的文件, 并跳转到指定行           |
