# pushd && popd
0. `cd -` 返回之前目录
1. `dirs` 显示当前目录栈，栈顶端永远是当前目录,`dirs -v`带index显示,`dirs -c`清空目录栈
2. `pushd <target_dir>` 将target_dir置于栈顶
3. `pushd` 置换目录栈最顶端两个目录
4. `popd` 删除栈顶目录(出栈)
5. `pushd -n` 选择`dirs -v`中的第n个目录
6. `popd -n` 删除`dirs -v`中的第n个目录
