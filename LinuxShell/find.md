# Find

`find <directory> [<tests>] [<options>] [<actions>]`

## Tests
### Name Test
* `-name <pattern>`
* `-iname <pattern>` 类似`-name`测试条件, 但是不区分大小写

### Type Test
`-type <file_type>`

| File Type | Description                   |
|-----------|-------------------------------|
| d         | Directory                     |
| f         | Regular file                  |
| l         | Symbolic link                 |
| b         | Block special device file     |
| c         | Character special device file |

注:
* block device: 以块为单位进行读取, 类似普通文件, 比如/dev/sda
* character device: 以字符为单位进行处理, 类似管道或者串口, 比如/dev/tty

### Size Test
* `-size [+-]<num>[unit]` +代表大于, -代表小于, 没有符号意味着精确匹配. 对于其他带上数值的测试也同理.
* `-empty` 匹配空文件或目录

| Character | Unit                                             |
|-----------|--------------------------------------------------|
| b         | 512-byte blocks, default if no unit is specified |
| c         | Bytes                                            |
| w         | 2-btyes words                                    |
| k         | kilobytes                                        |
| M         | Megabytes                                        |
| G         | Gigabytes                                        |

### Time Test
* change time:
    - `-cmin <n>` 匹配的文件/目录的内容或属性最后修改于在n分钟之前
    - `-ctime <n>` 匹配的文件/目录的内容或属性最后修改于在n天之前
    - `-cnewer <file>` 匹配的文件/目录的内容或属性最后修改时间早于给定的file
* modify time:
    - `-mmin <n>` 匹配的文件/目录的内容最后修改于在n分钟之前
    - `-mtime <n>` 匹配的文件/目录的内容最后修改于在n天之前
    - `-newer <file>` 匹配的文件/目录的内容最后修改时间早于给定的file, 可用于找出上次make后修改的源文件

### Other Test
* `-group <name>` 匹配的文件/目录属于一个组, 组可以用组名或者组ID来表示
* `-user <name>` 匹配的文件/目录属于某个用户, 用户可以通过用户名或者用户ID来表示
* `-nogroup` 匹配的文件/目录不属于一个有效的组
* `-nouser` 匹配的文件/目录不属于一个有效的用户, 可以用来查找属于删除账户的文件或检测黑客攻击行为
* `-perm <mode>` 匹配文件/目录的权限已经设置为指定的mode, mode可以用八进制或符号表示法 (perm=permission)
* `-inum <n>` 匹配的文件的inode号是n, 这对于找到某个特殊inode的所有硬链接很有帮助
* `-samefile <name>` 匹配和文件name享有同样inode号的文件

### Logical Operator
| Operator | Description                                                               |
|----------|---------------------------------------------------------------------------|
| -and     | 若两边的test都是真, 则匹配. 可简写为-a, 若没使用operator, 则默认使用-and    |
| -or      | 若两边的任一个test为真, 则匹配. 可简写为-o.                               |
| -not     | 若后面的test为假, 则匹配. 可简写为!                                       |
| ()       | 把test和operator组合起来形成更大的表达式, 圆括号对shell来说有特殊含义,      |
|          | 所以在命令行中使用它们时, 必须要用引号引起来, 才能作为实参传递给find命令, |
|          | 通常使用反斜杠字符来转义圆括号                                            |

类似一些编程语言`expr1 -operator expr2`中的`expr2`只有必要的时候才执行

## Actions
注意: action和test之间的顺序有影响, 下面命令会打印出所有文件名, 因为action本身也有真假, 会影响后续test或者action是否执行
```shell
find ~ -print -type f -name '*.bak'
```

### Predefined Actions
| Action           | Description                                                   |
|------------------|---------------------------------------------------------------|
| `-delete`        | Delete the currently matching file                            |
| `-ls`            | Perform the equivalent of `ls -dils` on the matching file     |
| `-fls <file>`    | Like `-ls`, but write the result to file                      |
| `-print`         | Default action, output the full pathname of the matching file |
| `-fprint <file>` | Print the full file name into file                            |
| `-print0`        | Like `-print`, but use null char as the delimiter             |
| `-quit`          | Quit once a match has been made                               |

### User-Defined Actions
| Action                    | Description                                            |
|---------------------------|--------------------------------------------------------|
| `-exec <command> {} ;`    | 执行指定的command, {} 指代匹配文件                     |
| `-exec <command> {} +`    | 类似`-exec`, 将多个匹配项组合到同一个command参数列表里 |
| `-execdir <command> {} ;` | 类似`-exec`, 但是在包含匹配文件的目录处执行command     |

注意: 因为花括号和分号对shell来说有特殊含义, 需要用用引号括起来, 或者转义

## Options

这些选项被用来控制find命令的搜索范围, 当构建find表达式时, 它们可能被其他的test和action包含
| Option             | Description                                                                                            |
|--------------------|--------------------------------------------------------------------------------------------------------|
| -depth             | 先处理目录中的文件, 再处理目录自身, 当指定-delete时, 会自动应用这个选项                                |
| -maxdepth <levels> | 当执行test和action时, 设置进入目录树的最大级别数                                                       |
| -mindepth <levels> | 在应用test和action之前, 设置进入目录树的最小级别数                                                     |
| -mount             | 指导find不要搜索挂载到其他文件系统上的目录                                                             |
| -noleaf            | 指导find不要基于搜索类Unix的文件系统作出的假设, 来优化它的搜索, 当扫描Windows文件系统, 或者CD-ROMs使用 |
