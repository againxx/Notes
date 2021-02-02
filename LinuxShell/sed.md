# Sed

## Substitute command: s
* Use `&` as the matched string
* `\1`-`\9` 用来表示捕获分组, 可以用在search pattern中, 而不一定只能用在replace string中

### Flags
* `g` 替换所有的匹配
* `<num>` 替换第num个匹配, num可以从1到512
* `<num>g` 替换从第num个开始的所有匹配

## Options
* `-r` 使用扩展的正则表达式, `+`,`()`等不用转义
* `-n` 抑制模式空间的自动输出
