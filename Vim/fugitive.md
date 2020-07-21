# Fugitive

Run an arbitrary git command and display any output. `:Git {args}` or `:G {args}`

## Gstatus / G
* `<C-n> / <C-p>` 上下移动到修改过的文件, 回车可打开该文件
* `-` 将文件移入或移出暂存区, normal和visual模式可用
* `s` 在unstaged上将所有文件移入缓存区, 在单个文件上将单个文件移入缓存区
* `u` 在staged上将所有文件移出缓存区, 在单个文件上将单个文件移出缓存区
* `U` 将所有文件移出缓存区
* `cc` 或 `:Gcommit` 用于提交暂存区中的文件
* `ca` amend the last commit and edit the message
* `ce` amend the last commit without editing the message
* `dd` 或 `:Gdiffsplit` 会打开两个分割窗口, 显示当前文件的diff信息, 具体分割方向由`diffopt`决定
* `dv` 或 `:Gvdiffsplit` 会打开两个垂直分割窗口, 显示当前文件的diff信息
* `ds` 或 `dh` 或 `:Ghdiffsplit` 会打开两个水平分割窗口, 显示当前文件的diff信息
* `dq` 退出diff模式
* `I` 或 `P` 对光标下的文件, 应用`git add --patch`或`git reset --patch`或`git add --intent-to-add`
* `g?` 显示命令帮助

## Gblame
`git blame` 可以快速提示每一行中修改操作的时间和用户

* `C`, `A` 和 `D` 调整窗口到指定大小(commit, author, date)
* `<Enter>` 打开所选提交的文件差异
* `o` 在水平分割窗口中打开所选提交的文件差异
* `O` 在新标签页中打开所选提交的文件差异
* `p` 在预览窗口中打开所选提交的文件差异
* `gq` 退出

## Git Index
Git index is where you put changes that you want to be included in the next commit.
You can open the index version of the current file by running first three commands of the following,
and open index version of any other file with the last command.
```
:Gedit
:Gedit :0
:Gedit :%
:Gedit :path/to/file
```

**Lifecycle of index file between two commits**
*  To begin with, the contents of the index and working copy files will be exactly the same as the most recent commit.
*  As you make changes to your working copy, its contents begin to diverge from those of the index file.
*  Staging a file updates the contents of the index file to match those of the working copy.
*  When you commit your work, it is the contents of the index file that are saved with that commit object.

![lifecycle of index file](https://gitee.com/againxx/image-storage/raw/master/images/index-lifecycle.png =740x)

## Gwrite & Gread
The `:Gread` and `:Gwrite` commands can either add a file to the index or reset the file, depending on where they are called from.

| Command   | Active Window | Affect        |
|-----------|---------------|---------------|
| `:Gwrite` | working copy  | stage file    |
| `:Gread`  | working copy  | checkout file |
| `:Gwrite` | index         | checkout file |
| `:Gread`  | index         | stage file    |

![Gwrite&Gread](https://gitee.com/againxx/image-storage/raw/master/images/Gread-Gwrite-matrix.png =740x)

## Others
| git                  | fugitive          | action                                                   |
|----------------------|-------------------|----------------------------------------------------------|
| `:Git rm --cached %` | `:GDelete`        | Delete the current file and the corresponding Vim buffer |
|                      | `:GRemove`        | Like `:GDelete`, but keep the empty buffer around        |
| `:Git mv % {dest}`   | `:GMove {dest}`   | Rename the current file and the corresponding Vim buffer |
|                      | `:GRename {dest}` | Like `:GMove` but operates relative to the parent dir    |

* `Gpush`
* `Gclog` 使用quickfix列表显示git log, 包含所有文件
* `[range]Gclog` 使用quickfix列表显示所选区域的不同commit间的修改
* `0Gclog` 使用quickfix列表显示当前文件的不同commit间的修改
* `Gllog` 使用locallist信息显示git log
* `Gvdiffsplit` 使用垂直分割的窗口显示diff信息
