# Argument List
参数列表 (argument list, arglist) 可以理解为用户可控的第二组文件列表, 主要用来同时在多个文件中执行同一操作.
每个参数列表项都在缓冲区列表中, 但不是每个缓冲区都在参数列表中.

* `:ar[gs]` 用于显示参数列表中的文件列表
* `:argdo` 对参数列表中的所有文件执行同一命令
* `:args {arglist_pattern}` 用于根据pattern定义参数列表, 并编辑其中的第一个文件
