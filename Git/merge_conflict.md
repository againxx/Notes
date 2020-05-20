# Merge & Conflict

## Conflict
当merge或rebase遇到冲突时, Git会在冲突文件中显示conflict markers
```
<<<<<<< HEAD
foo
=======
bar
>>>>>>> cb1abc6bd98cfc84317f8aa95a7662815417802d
```

有冲突的位置显示了两部分代码:
* the top half is the branch you a merging into
* the bottom half is from the commit that you are trying to merge in

What this means in practice if you are doing something like `git pull` (which is equivalent to a `git fetch` followed by a `git merge`) is:
* the top half shows your local changes
* the bottom half shows the remote changes, which you are trying to merge in

On the other hand, if you are doing something like `git rebase origin/master`, you are effectively trying to merge your local changes
"into" the upstream changes (by replaying them on top); that means:
* the top half shows the upstream changes
* the bottom half shows your local changes, which you are trying to merge in

**Markers之外的部分也可能发生了修改, 只不过没有冲突发生**

## 配置neovim作为merge工具
[Setting neovim as mergetool](https://www.grzegorowski.com/using-vim-or-neovim-nvim-as-a-git-mergetool)
```shell
git config --global merge.tool nvimdiff
git config --global diff.tool nvimdiff
git config --global merge.conflictstyle diff3
git config --global mergetool.prompt false
```

上述命令使用用户自定义的nvimdiff作为merge工具, 在合并时显示共同祖先(BASE), 并在打开nvimdiff时禁止弹窗提示

上述命令还使用nvimdiff作为diff工具, 可以使用`git difftool`来打开diff工具

**rebase时, commit不断的在rebase的分支上回放, 所以rebase时的BASE其实是在不断改变的**

## 窗口显示与操作

`git mergetool`来打开merge工具(neovim)

* 左边窗口(LOCAL): 当前分支的文件, conflict markers中的top part
* 中间窗口(MERGED): 合并结果, 即将要保存的输出结果
* 右边窗口(REMOTE): 另一分支中待合并的文件, conflict markers中的bottom part

* `d2o` 获得左边窗口的修改(maps defined by fugitive)
* `d3o` 获得右边窗口的修改(maps defined by fugitive)

**合并冲突时会在工作目录留下.orig文件, 合并结束后可将其删除**

## Other Configs
`git config --global rerere.enabled` 记录之前解决过的冲突, 当你再次遇到相同冲突时, 自动merge

## Other Reference
[Solving git merge conflicts with VIM](https://medium.com/prodopsio/solving-git-merge-conflicts-with-vim-c8a8617e3633)
[Vimcast fugitive](http://vimcasts.org/episodes/fugitive-vim-resolving-merge-conflicts-with-vimdiff/)
