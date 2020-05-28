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

## Options

## Actions
