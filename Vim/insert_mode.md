# Insert Mode
## Cues
* How to quit insert mode?
* What's the insert normal mode? How to enter it?
* What's the functionality of `<C-r>`? It stands for?
* How to increase / decrease indents?

## Notes
1. 从Insert Mode返回Normal Mode的三种方法:
    * `<Esc>`
    * `<C-c>`
    * `<C-[>`
2. Insert Mode常用快捷键:
    * `<C-h>` = Backspace
    * `<C-w>` 删除一个单词
    * `<C-u>` 删除至行首
    * `<C-o>` 进入Insert Normal Mode，可以执行一条Normal命令，之后返回Insert Mode
    * `<C-r>` 选择寄存器, 并将其中的内容复制到当前光标位置, 寄存器`=`可以进行快速的算数运算
    * `<C-r><C-p>` Insert the contents of a register literally and fix the indent
    * `<C-t>` 增加当前行的缩进, 不需要将光标移动到行首
    * `<C-d>` 减少当前行的缩进
