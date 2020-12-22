# Undo

[Video Version](https://www.youtube.com/watch?v=FdZecVxzJbk&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx&index=2)

## Undo in Working Directory
* `git restore <file>, git checkout <file>, git checkout -- <file>` 丢弃工作区的修改
* `git clean -df` 丢弃untracked file和untracked directory(-d), `-f`表示force, 还可以使用`-i`进行交互式clean

## Undo in Staging Area (Index)
* `git reset <file>` 不缓存文件
* `git restore --staged <file>` 同上
* `git reset` 不缓存所有文件

## Undo Commit
* `git commit --amend -m <message>` 可以修正上次提交的信息, 注意这样会修改commit的hash值, 最好只在push之前进行
* `git commit --amend` 可以将额外的staged files纳入最近一次提交
* `git cherry-pick <hash1> <hash2> ...` 将一个分支的commits(可以是多个)复制到另外一个分支
    - 默认会在当前分支上新建N个commits, 与原始分支对应
    - `git cherry-pick <hash> -n` 则会将其他分支的commit转移到缓存区, 然后可以再进一步手动commit
* `git reset --soft <hash>` 将之前一个或多个commit的修改回退到staging area
* `git reset [--mixed] <hash>` 将之前commit的修改回退到working directory, 因为即修改了commit object又修改了index, 所以被称为mixed
* `git reset --hard <hash>` 将之前一个或多个commit的修改丢弃, tracked file的修改会全部消失, untracked file还会存在
* `git reflog` 会列出之前所有引用过的分支记录(hash), 可以利用这个hash值来撤销reset操作
* `git checkout <hash>` 回到reset撤销操作之前的commit, 这个时候会处于detached HEAD状态，需要额外创建一个分支来保存它,
checkout本身也可以切换到任何历史提交
* `git checkout <hash> <files>` 将中一个或多个文件回退到历史版本, 丢弃修改后的版本(即历史版本)会放在staging area
* `git revert <hash>` 在别人已经pull之前的commit的情况下, revert会生成一个新的commit, 撤销到之前commit的状态,
当你再次push之后, 别人就能同步你对commit的撤销了
* `git reflog` 拥有比`git log` 更细粒度的log记录, reflog的记录针对当前分支
* 使用`git reset --hard <hash>` 操作从reflog获得的hash, 即可完全回退到该历史节点

## Examples
* `git reset HEAD` 将staging area的内容全部回退到working directory
* `git reset --soft HEAD~5` 将最近五次的commit回退到staging area
