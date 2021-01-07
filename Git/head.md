# HEAD

## What is HEAD
git中存在两种引用
* branch引用: 指向某一个branch的最新的commit
* HEAD引用: 指向某个branch
* `git show HEAD` 可以显示HEAD引用当前指向的commit

## Ancestry References
* `HEAD~~` : 2 commits older than HEAD
* `HEAD~2` : 2 commits older than HEAD
* `HEAD^^` : 2 commits older than HEAD
* `HEAD^2` : the second parent of HEAD, if HEAD was a merge, otherwise illegal

If HEAD was a merge, then
* **first parent** is the branch into which we merged,
* **second parent** is the branch we merged.

![Referencing commits using ~ and ^](https://gitee.com/againxx/image-storage/raw/master/images/git-graph.svg)

## reflog
* `git reflog` 可以查看HEAD所指位置的历史记录
* 可以用`HEAD@{n}`来引用HEAD历史上的位置
* `git show master@{yesterday}` 查看master分支昨天的位置
* `git log -g master` 用类似`git log`的输出格式输出reflog信息
* reflog信息是针对本地你自己的操作的, 可以理解成git版的shell history

## Detached HEAD
* 当我们`git checkout <sha1_hash>` 到某个commit时,
  此时HEAD指针不再指向任何一个branch指针而是指向一个具体的commit, 此时即称为`detached HEAD`
* 此时可以在`detached HEAD`上继续提交分支, 如果之后checkout到了已有分支, 则这些没有任何指针指向的分支则成为`detached commit`

## Reference
* [Using Git: What is a "Detached HEAD"? - YouTube](https://www.youtube.com/watch?v=GN36mrrM12k)
* [PaulBoxley.com – Git caret and tilde](http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde)
* Pro Git v2: 7.1 Git Tools - Revision Selection
