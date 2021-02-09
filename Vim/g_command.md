# G Command

* `Ctrl-g` 显示当前行号、列号等信息
* `g<` 重复上一条命令的输出
* `g&` 重复上一次的替换命令, 会利用前一次的search结果
* `g;`和`g,` 正向或反向遍历改变列表
* `ga` 显示当前字符的ascii码, 重映射为`<leader>va`, 当前`ga`是EasyAlign
* `gJ` 连接上下两行, 但是维持下一行的格式, 而不是用一个空格分割
* `gF` 跳转到文件名对应文件的对应行`<file_name>:<line_num>`
* `<num>g_` 跳转到第num行的末尾, 包含当前行
* `gq` format by motion or visual selected
* `gv` 重新高亮之前的选区
* `gn` / `gN` visual select next match, or extend selection region to the next match
* `gi` 跳转到最后一次离开插入模式的地方并进入插入模式
