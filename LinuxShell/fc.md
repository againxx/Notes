# fc 列出、编辑和重新执行历史命令

fc命令是buildin的, 意味着fc来自shell而不是操作系统. 因此, fc可以根据所使用的shell略有不同.
fc命令存在于大多数shell, 包括bash, zsh和ksh.

* `fc` 打开文本编辑器编辑并运行输入到shell的最后一个命令 (编辑器可通过`FCEDIT`环境变量指定)
* `fc -l`列出之前的命令, 每条命令前带有相应的编号
* `fc -l <num>` 从num指定的编号开始查看
* `fc -l <num1> <num2>` 查看一个范围
* `fc -ln` 不显示序号, `-n`参数
* `fc <num>` 编辑并执行之前的命令
* `fc -e nvim` 动态设置编辑器
* fzf-Ctrl-r + vi-mode, 更实用
