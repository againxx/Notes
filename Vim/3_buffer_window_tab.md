# Buffer & Window & Tab

## Buffer
Buffer即内存中待编辑的文件，例`vim .vimrc .zshrc`会同时打开两个buffer
操作Buffer | Description
:-|:-
`:ls, :buffers` | 列出所有的buffer
`:bd[elete]` | 关闭当前的buffer
`:bn[ext]` | 切换到下个buffer
`:bp[revious]` | 切换到上个buffer
`:b<N>` | 切换到第N个buffer，`:ls`可以显示buffer的index

## Window
Window是可视化buffer的一个视点，即将屏幕分窗
操作Window | Description
:-|:-
`:split, Ctrl-w + s` | 水平分割窗口
`:vsplit, Ctrl-w + v` | 垂直分割窗口
`Ctrl-w + hjkl` | 在不同窗口间移动
`:q[uit], Ctrl-w + q` | 关闭当前窗口
`:c[lose], Ctrl-w + c` | 关闭当前窗口，只剩最后一个窗口时不会关闭
`Ctrl-w + o` | 仅保留当前窗口

## Tab (layout)
Tab是用来配置不同Window布局的
操作Tab | Description
:-|:-
`:tabnew [file_path], :tabe[dit] [file_path]` | 打开空的新标签或者在新标签里打开文件
`gt, tabn[ext]` | 切换到下个标签
`gT, tabp[revious]` | 切换到上一个标签
`<N>gt` | 切换到第N个标签
`tabc[lose]` | 关闭当前标签
`tabo[nly]` | 仅保留当前标签
