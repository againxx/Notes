# Branch

## Check branch state
* `git branch` 查看当前本地分支
* `git branch -a` 查看当前本地和远程分支
* `git branch -r` 查看remote-tracking分支
* `git branch --merged` 查看当前HEAD指针包含的分支，如果一个分支merge成功，可在此处查看到
* `git branch -vv` 可以查看当前本地分支的upstream

## Create & Switch
* `git branch <name>` 创建分支
* `git checkout <name>, git switch <name>` 切换分支
* `git checkout -` 切换到最近的分支
* `git checkout -b <name>, git switch -c <name>` 创建并切换分支
* `git checkout --track origin/<name>` 切换到远程同名分支并设置本地同名分支跟踪它
* 切换分支时若有工作区或暂存区有文件会被覆盖, 则不能切换分支
* 切换分支时有些文件可能会出现或者消失

## Merge
* `git merge <target_branch>` 合并分支
* `git merge --abort` 终止合并分支, 将工作区恢复到当前branch的最后一次commit的状态
* `git merge --squash <target_branch>` 将target branch的所有commit压缩成一个commit合并到当前分支中

## Push
`git push -u <remote_name> <branch_name>` 将本地分支推送到远程仓库, -u表示添加upstream reference, 之后只用`git push origin master`即可

> When a local branch has an "upstream branch" configured for it, it will by default pull from and push to that remote branch.
> A local branch that has an "upstream branch" set on it is referred to as a "tracking branch", so it's easy to confuse with
> remote-tracking branches due to the similar terminology

## Pull
* `git pull <remote_name> <branch_name>` 多人合作时应记得在push之前pull

## Delete
* `git branch -d <name>` 删除本地分支
* `git branch -D <name>` 如果要删除的分支没有完全merge, 需要使用-D来强行删除
* `git push origin --delete <name>` 删除远程分支, 同时会删除remote-tracking分支
* `git branch -dr <remote-tracking_branch_name>` 删除remote-tracking branch(连接本地branch和远程branch的追踪branch) 
* `git fetch --all --prune` 如果远程分支被删除了, 记得在其他机器上运行这一句来同步(obsolete remote-tracking branches)
* `git remote update <remote_name>; git remote prune <remote_name>` 删除本地过时的分支(即远程仓库不存在的分支), 被`git fetch <remote_name> --prune`替代

**Note:**
There are three different branches to delete
1. local branch `X`
2. remote origin branch `X`
3. local remote-tracking branch `origin/X` that tracks the remote X

![remote tracking branch](https://gitee.com/againxx/image-storage/raw/master/images/NLAqw.png)

[great answer about three different branches](https://stackoverflow.com/a/23961231)
