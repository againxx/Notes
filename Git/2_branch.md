# Branch

## Check branch state
* `git branch` 查看当前本地分支
* `git branch -a` 查看当前本地和远程分支
* `git branch --merged` 查看当前HEAD指针包含的分支，如果一个分支merge成功，可在此处查看到

## Create & Switch
* `git branch <name>` 创建分支
* `git checkout <name>, git switch <name>` 切换分支
* `git checkout -b <name>, git switch -c <name>` 创建并切换分支

## Merge
`git merge <name>` 合并分支

## Delete
* `git branch -d <name>` 删除分支
