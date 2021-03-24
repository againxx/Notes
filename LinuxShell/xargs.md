# xargs 从标准输入构建参数并执行命令

`xargs [options] <command> [initial-arguments]`

**用法:**

从标准输入读入由空格或者新行分割的参数项\<append-arguments\>，并依次执行  
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

`-L <number>, -l<number>, --max-lines=<number>`  
每number行调用一次command, 注意与`-n`的区别, `-l`相当于只以新行作为分割来执行若干次command, 但是构造每个command
的参数列表时, 还是会考虑其他的分隔符

`-p --interactive`  
交互式的方式运行每条命令, 需要手动输入Y/N, 可以查看xargs构造的命令来debug

`-I <replace_str>`  
将初时参数中的replace str用从标准输入读到的参数替代, 可以用于构造标准输出的参数不在最后的命令, 但是注意该参数隐含-L 1, 所以一次只替换一行

## Examples
* `ls | xargs wc -l` Counting lines for current directory, 注意`wc`可以直接接受标准输入, 不需要嵌套`xargs`
* `pip freeze --local | grep -v '^\-e' | cut -d = -f 1 | xargs -n1 pip install -U` Update all pip packages
* `xargs rm < install_manifest.txt` 删除cmake install安装的文件
* `cat install_manifest.txt | xargs -l1 dirname | sudo xargs rmdir -p` 删除cmake install留下的空目录
    - 可能会有很多报错, 因为要删除的目录非空, 可以通过`rmdir`的`--ignore-fail-on-non-empty`参数来抑制错误输出
