# Log

* `git log` 查看commit历史，每个commit会带有一个40个字符长的独一无二的标识符(commit ref/hash)
* `git log -<num>` 查看最近num次提交的历史
* `git log --oneline` 每个commit历史只用一行显示，包含缩短的commit ref和commit message
* `git log --stat` 查看提交历史以及相应的修改记录（文件名，修改的行数等）
* `git log --stat -- <file>` 只查看与某个file相关的提交历史
* `git log -p/--patch` 查看具体的代码修改历史（类似diff的方式展现）
* `git log -p/--patch -U<n>` diffs with <n> lines of context
* `git log --graph` 以ascii码树的形式展示commit历史
* `git log --grep` 仅显示包含grep pattern的commit

## Commit Ranges

### double dot
用来比较两个分支之间的差异, 即一个分支有而另一个分支没有的提交
* `git log master..dev` 显示dev分支有而master分支没有的提交
* `git log dev..master` 显示master分支有而dev分支没有的提交
* `git log origin/master..[HEAD]` 显示HEAD分支和远程master分支之间的差异, HEAD是可缺省的, 可以帮助了解哪些提交将推送到远端
