# String

* Vim中用`.`来连接多个string, `+`运算会将string转换成number
* string和number(整数)运算时会装换成number, 比如"2 cat"变成2, "10.10"会转换成10, 而不是float
* `echo`会按转义字符正常的方式显示字符串, 而`echom`会输出字符串原本的形式(包含一些vim特有的字符)
* 单引号包围的字符串为字面值字符串(类似python的r string), 只有两个单引号会被转义成一个单引号
* 字符串作为条件表达式, 除非开头包含非零数字, 否则都为false

## String Functions
* `strlen()` / `len()`
* `split("one,two,three", ",")` / `split("one two three")` -> ['one', 'two', 'three']
* `join(['foo', 'bar'], "...")`
* `join(split("foo bar"), ";")` -> 'foo;bar'
* `tolower("Foo")`
* `toupper("Foo")`
