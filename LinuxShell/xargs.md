# xargs 从标准输入构建参数并执行命令

`xargs [options] <command> [initial-arguments]`

**用法:**

从标准输入由空格或者新行分割的参数项\<append-arguments\>，并依次执行  
`<command> [initial-arguments] <append-arguments>`

**Options:**

`-n <max-args>, --max-args=<max-args>`  
每条命令最多使用max-args个参数

`-d <delim>, --delimiter=<delim>`  
指定分隔输入参数的字符

`-0, --null`  
用null来分隔输入参数，可配合`find -print0`使用

## Examples
`ls | xargs wc -l` Counting lines for current directory
