# Log

* `git log` 查看commit历史，每个commit会带有一个40个字符长的独一无二的标识符(commit ref/hash)
* `git log -<num>` 查看最近num次提交的历史
* `git log --oneline` 每个commit历史只用一行显示，包含缩短的commit ref和commit message
* `git log --stat` 查看提交历史以及相应的修改记录（文件名，修改的行数等）
* `git log --stat -- <file>` 只查看与某个file相关的提交历史
* `git log --patch` 查看具体的代码修改历史（类似diff的方式展现）
* `git log --graph` 以ascii码树的形式展示commit历史
