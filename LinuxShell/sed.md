# Sed

## Pattern space & Hold space

## Substitute command: s
* Use `&` as the matched string
* `\1`-`\9` 用来表示捕获分组, 可以用在search pattern中, 而不一定只能用在replace string中

### Flags
* `g` 替换所有的匹配
* `<num>` 替换第num个匹配, num可以从1到512
* `<num>g` 替换从第num个开始的所有匹配

## Single line commands
### Accept zero / one address
* `=` 打印当前行号
* `a <text>` append text, 可以用`\` 断行来输入多行文本
* `i <text>` insert text, 可以用`\` 断行来输入多行文本
* `q [exit-code]` 立即退出脚本的执行, 如果有auto-print的话, 当前的pattern space中的内容会被打印
* `Q [exit-code]` 立即退出脚本的执行, 不打印当前pattern space中的内容
* `r <filename>` 从文件中读入附加在行后
* `R <filename>` 从文件中读入一行附加在行后, 每调用一次读入一行

### Accept address ranges
* `{}` contains a block of commands
* `b [label]` 分支跳转到label处, 如果没有label就跳转到脚本结尾

## Label
* `:label` 指定label用于`b` 和 `t` 命令

## Options
* `-e` 添加要执行的commands
* `-f` 从sed脚本文件读入命令
* `-i[suffix]` 原地修改文件, 如果指定suffix的话则会使用suffix来生成备份文件
* `-r / -E` 使用扩展的正则表达式, `+`,`()`等不用转义, sed默认是基础正则表达式
* `-n` 抑制模式空间的自动输出(auto-print), 该输出会在每次清空模式空间, 重新载入新行时进行
* 如果没有`-e` 和 `-f` 选项, 第一个非选项的参数将作为sed脚本解释, 其余的参数都将作为文件名解释
