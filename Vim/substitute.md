# Substitute

`:[range]s/<find-this>/<replace-with-this>/[flags] [count]`

其中range、flags和count是可选的

![Substitute Summary](https://gitee.com/againxx/image-storage/raw/master/images/vim-substitute.jpg =750x)

## Flags
* `g` 全局替换, 即将匹配到的所有项都替换掉, 而不仅仅是第一个
* `c` 每次替换前确认一下
* `e` 没有匹配项时不显示错误
* `i` 忽略大小写
* `I` 区分大小写
* `&` 重用上一次的选项, vim有用(neovim下好像有问题)
* `n` 不实际替换, 而是显示会影响多少匹配项
* 选项可根据需求结合使用(除`i`和`I`之外)

## Replace Special
* 注意magic模式下`&`表示整体匹配模式(通`\0`), 用`\&`表示普通的&
* `\0` 用整体匹配的模式替换
* `\<n>` 用第n个分组匹配的模式替换(用`\(\)`来分组)
* `~` 用之前一次substitute的string来替换, 用`\~`表示普通的~
* `\u` 下一个字符大写
* `\U` 之后的字符大写直到`\E`
* `\l` 下一个字符小写
* `\L` 之后的字符小写直到`\E`
* `\e` 结束`\u`, `\U`, `\l` and `\L`
* `\E` 同 `\e`
* `<CR>` 在此处分行 (用`Ctrl-v + <Enter>`输入)
* `\r` 同上
* `\n` 插入一个`<NL>`, 并不会分行
* `\=` 当replace部分的以`\=`开头时, 接下来部分会作为表达式处理

## Replace Expression
* 上述的的特殊含义的字符只有`<CR>`还可以使用
* 当表达式的结果是`List`的时候, 会用换行符将他们连接起来作为替换部分(即每一项变成一行)
* 用`submatch(<n>)`获得匹配的分组(即之前的`\0`, `\1`...)

## 其他技巧
### 替换字符串中包含/
Linux风格的路径中包含/符号, 可以使用反斜杠\进行转义, 也可以修改替换命令的分割符,
比如`:s+path/to/dir+path/to/other/dir+gc`中的命令分隔符被改成了+, 等价于`:s/path\/to\/dir/path\/to\/other\/dir/gc`

### 替换完整单词
使用单词界定符`\<`和`\>`, 例如`:s/\<animal\>/creature/g` 可将animals排除
### 省略查找字符串
会使用上一次的search结果(/ ? * #)
