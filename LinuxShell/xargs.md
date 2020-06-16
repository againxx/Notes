# xargs 从标准输入构建参数并执行命令

`xargs [options] <command> [initial-arguments]`

**用法:**

从标准输入由空格或者新行分割的参数项\<append-arguments\>，并依次执行  
`<command> [initial-arguments] <append-arguments>`

**Options:**

`-n <max-args>, --max-args=<max-args>`  
每条命令最多使用max-args个参数

`-d <char>, --delimiter=<char>`  
指定分隔输入参数的字符

`-0, --null`  
用null来分隔输入参数，可配合`find -print0`使用

`--show-limits`  
查看command line的上限, 若指定的参数数量超过该上限, `xargs`会每次用最大参数数量执行command, 直到所有参数均消耗完

## Examples
* `ls | xargs wc -l` Counting lines for current directory, 注意`wc`可以直接接受标准输入, 不需要嵌套`xargs`
* `pip freeze --local | grep -v '^\-e' | cut -d = -f 1 | xargs -n1 pip install -U` Update all pip packages
