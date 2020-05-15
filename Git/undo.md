# Undo

[Video Version](https://www.youtube.com/watch?v=FdZecVxzJbk&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx&index=2)

## Undo in Working Directory
* `git restore <file>, git checkout <file>, git checkout -- <file>` 丢弃工作区的修改
* `git clean -df` 丢弃untracked file和untracked directory(-d), `-f`表示focus, 还可以使用`-i`进行交互式clean

## Undo Commit
* `git commit --amend -m <message>` 可以修正上次提交的信息, 注意这样会修改commit的hash值, 最好只在push之前进行
* `git commit --amend` 可以将额外的staged files纳入最近一次提交
* `git cherry-pick <hash>` 将一个分支的commit复制到另外一个分支
* `git reset --soft <hash>` 回退到之前的commit, 提交的修改会返回到staging area
* `git reset [--mixed] <hash>` 回退到之前的commit, 提交的修改会返回到working directory
* `git reset --hard <hash>` 回退到之前的commit, tracked file的修改会全部消失, untracked file还会存在
* `git reflog` 会列出之前所有引用过的分支记录(hash), 可以利用这个hash值来撤销reset操作
* `git checkout <hash>` 回到reset撤销操作之前的commit, 这个时候会处于detached HEAD状态，需要额外创建一个分支来保存它,
checkout本身也可以切换到任何历史提交
* `git revert <hash>` 在别人已经pull之前的commit的情况下, revert会生成一个新的commit, 撤销到之前commit的状态,
当你再次push之后, 别人就能同步你对commit的撤销了
