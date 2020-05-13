# Stash

Store the changes in working directory in temporary place

* `git stash save "<some message>"` stash工作区的修改
* `git stash push` 同stash save
* `git stash list` 列出所有stash的记录
* `git stash apply <stash index>` 应用stash, stash index通过`stash list`列出, 应用后stash记录将继续保留
* `git stash pop` 应用最近一次stash, 应用后stash记录被丢弃
* `git stash drop <stash index>` 抛弃stash, 默认抛弃第一个stash
* `git stash clear` 清除所有的stash
* stash可以跨越多个分支, 当在错误的分支上进行了修改, 可以先stash save, 然后切换到正确的分支上再stash pop
