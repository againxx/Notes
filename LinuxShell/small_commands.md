# Useful small commands
1. `cd` 返回~目录
2. `cd -` 返回之前的工作目录
3. `cd ~<user_name>` 前往user_name的家目录
4. `touch` 创建新文件/更新修改（访问）时间，访问时间(atime)目前已经不随`cat`等命令更新了
5. `stat` 显示文件信息（三种时间）
    * atime: last access time, modern linux tend to optimize atime usage to avoid frequently write to disk
    * ctime: last change time, which corresponds to metadata changes - typically that's file ownership (username and/or group) and access permissions, 
      also get updated if the file contents got changed
    * mtime: last change to file contents
6. `gdebi` deb包安装工具，可处理依赖
7. `head -n <num_lines>` 显示文件的头num_lines行，默认显示10行
8. `tail -n <num_lines>` 显示文件的尾num_lines行，默认显示10行
9. `df -h` 显示文件系统的使用情况
10. `du -h` 显示当前目录下文件的硬盘空间使用情况
11. `ncdu` 交互式的du
12. `duf` 显示所有device和文件系统的使用情况
13. `more` 类似`cat`，但仅显示一部分 e.g `ls -alh | more`
14. `less` 类似`more`，但是支持更多的vim快捷键
15. `<command 1> | <command 2>` 管道符把前一个命令的标准输出作为后一个命令的标准输入。
16. `<command 1> |& <command 2>` 管道符把前一个命令的标准输出和错误输出同时作为后一个命令的标准输入。
    很多命令无法直接从标准输入读入参数（如rm，touch等），这时应在`|`后衔接`xargs`
17. `seq [<first>] [<increment>] <last>` 输出一个数字序列
18. `wc` 输出newline, word, and byte的计数
19. `tee` 能将标准输出复制到文件，并同时显示到屏幕
20. `tree` 以树状结构输出目录内容
21. `cut` 能根据分割符对字符串进行分割, 例如`cut -d = -f 1`对等号进行分割, 并且只取分割后的第一项
22. `neofetch` 能显示一些系统相关的基本信息，包括颜色palette
23. `timeout` 运行命令一段时间, 如果到时间了该命令还未完成则终止它
24. `whatis` 可以获得对一个命令的简短描述
25. `free` 可以获得简单的内存使用情况
26. `eog` (Eye of Gnome) 可以用来在终端中打开图片
27. `evince` 可以在终端中打开pdf
28. ` &` 添加在命令结尾来使命令后台运行
29. `locate` 快速搜索路径名数据库, 并输出与给定字符串相匹配的文件名
    - `locate` 命令使用的数据库由`updatedb`维护, `updatedb` 会每隔一天运行一次, 也可手动运行来更新`locate`数据库
30. `cal`
31. `free` 显示内存的使用情况
32. `ctrl-d` = exit
33. `faketime` 为某个command提供一个虚假的时间
34. `nmtui` 网络管理工具, 可以在终端连接Wi-Fi
35. `sudo !!` 可以快速使用sudo重新运行上一次的命令, 特别适合忘记加sudo的时候
36. `!$ / Esc + .` 可以快速使用上一次命令的最后一个参数
37. `mtr` 比ping更详细的网络包跟踪软件
38. `alt-.` 插入上一条命令的参数到当前位置
39. `strings` 可以打印二进制文件中的字符串, 可以用来查看二进制的gcc编译版本`strings -a <binary/library> |grep "GCC: ("`
40. `lsb_release` ubuntu上列出发行版信息
