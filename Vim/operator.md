# Operator

* `c` 修改(change) 
* `d` 删除(delete)
* `y` 抽出(yank)到寄存器
* `~` 变换大小写(只有当'tildop'置位时有效, 否则不作为操作符)
* `g~` 变换大小写
* `gu` 变为小写
* `gU` 变为大写
* `!` 通过外部程序过滤
* `=` 通过'equalprg'(若为空, C-indenting)过滤
* `gq` 文本排版
* `gw` 文本排版, 不移动光标
* `g?` ROT13编码 
* `>` 右移
* `<` 左移
* `zf` 定义折叠
* `g@` 调用'operatorfunc'选项定义的函数

## Other Description

* 如果动作包括一个次数而操作符之前也有一个的话，两者相乘。因此，"2d3w" 删除六个单词。
