# Useful small commands
0. `cd` 返回~目录
1. `touch` 创建新文件/更新修改（访问）时间，访问时间(atime)目前已经不随`cat`等命令更新了
2. `stat` 显示文件信息（三种时间）
3. `gdebi` deb包安装工具，可处理依赖
4. `head -n <num_lines>` 显示文件的头num_lines行，默认显示10行
5. `tail -n <num_lines>` 显示文件的尾num_lines行，默认显示10行
6. `df -h` 显示文件系统的使用情况
7. `more` 类似`cat`，但仅显示一部分 e.g `ls -alh | more`
8. `less` 类似`more`，但是支持更多的vim快捷键
9. `<command 1> | <command 2>` 管道符把前一个命令的标准输出作为后一个命令的标准输入。
很多命令无法直接从标准输入读入参数（如rm，touch等），这时应在`|`后衔接`xargs`
10. `seq [<first>] [<increment>] <last>` 输出一个数字序列
11. `wc` 输出newline, word, and byte的计数
12. `tee` 能将标准输出复制到文件，并同时显示到屏幕
13. `tree` 以树状结构输出目录内容
