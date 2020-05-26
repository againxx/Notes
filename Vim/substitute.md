# Substitute

`:[range]s/<find-this>/<replace-with-this>/<flags>`

其中range和flags是可选的

## Flags
* `g` 全局替换, 即将匹配到的所有项都替换掉, 而不仅仅是第一个
* `c` 每次替换前确认一下
* `e` 没有匹配项时不显示错误
* `i` 忽略大小写
* `I` 区分大小写
* `&` 重用上一次的选项, vim有用(neovim下好像有问题)
* `n` 不实际替换, 而是显示会影响多少匹配项
* 选项可根据需求结合使用(除`i`和`I`之外)

## 其他技巧
### 替换字符串中包含/
Linux风格的路径中包含/符号, 可以使用反斜杠\进行转义, 也可以修改替换命令的分割符,
比如`:s+path/to/dir+path/to/other/dir+gc`中的命令分隔符被改成了+, 等价于`:s/path\/to\/dir/path\/to\/other\/dir/gc`

### 替换完整单词
使用单词界定符`\<`和`\>`, 例如`:s/\<animal\>/creature/g` 可将animals排除
### 省略查找字符串
会使用上一次的search结果(/ ? * #)
