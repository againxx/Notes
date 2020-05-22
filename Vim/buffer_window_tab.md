# Buffer & Window & Tab

## Buffer
Buffer即内存中待编辑的文件，例`vim .vimrc .zshrc`会同时打开两个buffer
| 操作Buffer      | Description                                                                                  |
|:----------------|:---------------------------------------------------------------------------------------------|
| `:ls, :buffers` | 列出所有的buffer                                                                             |
| `:bd[elete]`    | 关闭当前的buffer                                                                             |
| `:bn[ext]`      | 切换到下个buffer                                                                             |
| `:bp[revious]`  | 切换到上个buffer                                                                             |
| `:bf[irst]`     | 切换到第一个buffer                                                                           |
| `:bl[ast]`      | 切换到最后一个buffer                                                                         |
| `:b<N>`         | 切换到第N个buffer，`:ls`可以显示buffer的index                                                |
| `:b {bufname}`  | 切换到可以由{bufname}标示的缓冲区, {bufname}只需包含文件路径中足以唯一标识此缓冲区的字符即可 |
| `bufdo`         | 在`:ls`列出的所有缓冲区上执行Ex命令                                                          |
| `Ctrl-^`        | 切换到最近编辑的buffer，可以用于两个文件之间轮流切换                                         |

## Window
Window是可视化buffer的一个视点，即将屏幕分窗
| 操作Window             | Description                                      |
|:-----------------------|:-------------------------------------------------|
| `:split, Ctrl-w + s`   | 水平分割窗口                                     |
| `:vsplit, Ctrl-w + v`  | 垂直分割窗口                                     |
| `CTRL-w + hjkl`        | 在不同窗口间移动, 自定义为`ALT-hjkl`             |
| `:q[uit], Ctrl-w + q`  | 关闭当前窗口                                     |
| `:c[lose], Ctrl-w + c` | 关闭当前窗口，只剩最后一个窗口时不会关闭         |
| `CTRL-w + o`           | 仅保留当前窗口                                   |
| `CTRL-w_r`             | 调整窗口的位置, 循环调整                         |
| `CTRL-w_R`             | 调整窗口的位置, 反向循环调整                     |
| `CTRL-w_x`             | 交换当前窗口和下一个窗口                         |
| `CTRL-w_HJKL`          | 调整窗口的位置, 指定上下左右                     |
| `CTRL-w_hjkl`          | 在上下左右分割窗口, 并将光标置于对应窗口(自定义) |
| `CTRL-w__`             | 垂直方向最大化当前窗口                           |
| `CTRL-w_<bar>`         | 水平方向最大化当前窗口                           |
| `CTRL-w_=`             | 使各窗口均等                                     |
| `CTRL-w_<>`            | 左右调整窗口大小, 自定义为`ALT-,.`               |
| `CTRL-w_+-`            | 上下调整窗口大小, 自定义为`ALT-=-`               |

## Tab (layout)
Tab是用来配置不同Window布局的
| 操作Tab                                       | Description                          |
|:---------------------------------------------:|:------------------------------------:|
| `:tabnew [file_path], :tabe[dit] [file_path]` | 打开空的新标签或者在新标签里打开文件 |
| `gt, tabn[ext]`                               | 切换到下个标签                       |
| `gT, tabp[revious]`                           | 切换到上一个标签                     |
| `<N>gt`                                       | 切换到第N个标签                      |
| `tabc[lose]`                                  | 关闭当前标签                         |
| `tabo[nly]`                                   | 仅保留当前标签                       |
