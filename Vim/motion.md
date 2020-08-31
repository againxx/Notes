# Motion

## Horizontal Motion
* `-` 上一行的行首非空白字符
* `+` 下一行的行首非空白字符
* `_` 当前行的行首非空白字符
* `^` 当前行的行首非空白字符
* `0` 当前行的第一个字符
* `$` 当前行的最后一个字符
* `g_` 当前行的行尾非空白字符
* `<count>|` 当前行的指定列

## Vertical Motion
* `{` and `}`
* `<count>%` 跳转到当前buffer的百分之多少
* `<line_num>gg` / `<line_num>G`
* `:<line_num>` 跳转到指定行号, 由于可以修改对于三位数以上的行号有优势
* `:+/-<line_num>` 跳转到相对指定行号

## Screen Motion
* `zt`
* `zz`
* `zb`
* `z<Enter>` 类似`zt`但是将光标置于行首
