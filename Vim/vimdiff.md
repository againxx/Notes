# Vimdiff

`vimdiff <file1> <file2> ...`

`nvim -d <file1> <file2> ...`

## 快捷键
* `[c / ]c` 在多处修改之间跳转
* `do` 或 `:diffg[et]` 将文件的修改应用当前窗口中的文件 (**do**表示diff obtain)
* `dp` 或 `:diffpu[t]` 将当前窗口中的文件修改推送给另一个文件 (**dp**表示 diff put)
* `:%diffget / :%diffput` 将一个文件整体复制到另外一个文件中
* `:dif[fupdate]` 手动更新差异高亮和折叠
* 当有两个以上的文件比较差异时, `:diffget`和`:diffput`需要跟一个表示buffer编号或者文件名的参数
