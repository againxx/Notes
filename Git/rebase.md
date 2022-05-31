# Rebase

Rebase allows one branch to be relocated farther down the history track.

Workflow using rebase:
1. `git checkout feature-branch`
2. `git rebase master`
3. `git checkout master`
4. `git rebase feature-branch` or `git merge feature-branch`

`git pull --rebase` fetch完后调用rebase而不是merge

## Difference between Merging and Rebasing

* Merging will stuff all changes from feature branch into one large merge commit
* Git tree may become complex by using merging

![Merging](http://images.againxx.cn/git-merge-graphic.png =750x)

* Rebasing will take all of the commits on feature branch and move them on top of master commits
* Nice clean tree with all your commits laid out nicely in a row

![Rebasing](http://images.againxx.cn/git-rebase-graphic.png =750x)

## Options for Rebase
| Option              | Description                                          |
|---------------------|------------------------------------------------------|
| --continue          | continue after resolving merge conflict              |
| --abort             | abort current rebase                                 |
| --show-current-path | 显示当前正在应用第几个commit, 以及该commit的修改信息 |

## rebase -i
`git rebase --interactive, -i` Git中的"魔术时光机", 允许在rebase时对修订历史记录进行复杂的修改
当你运行`git rebase -i`时, 你会进入一个编辑器会话, 其中列出了所有正在被变基的提交, 以及可以对其执行的操作的多个选项. 默认的选择是选择(Pick).

* Pick: 会在你的历史记录中保留该提交.
* Reword: 允许你修改提交信息, 可能是修复一个错别字或添加其它注释.
* Edit: 允许你在重放分支的过程中对提交进行修改.
* Squash: 可以将多个提交合并为一个.
* 你可以通过在文件中移动来重新排序提交.

## Rebasing Caveats
It can also be dangerous if you’re working on a shared branch with other developers because of how Git rewrites commits when rebasing.
