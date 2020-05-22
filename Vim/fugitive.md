# Fugitive

Run an arbitrary git command and display any output. `:Git {args}` or `:G {args}`

## Gstatus / G
* `<C-n> / <C-p>` 上下移动到修改过的文件, 回车可打开该文件
* `-` 将文件移入或移出暂存区, normal和visual模式可用
* `s` 在unstaged上将所有文件移入缓存区, 在单个文件上将单个文件移入缓存区
* `u` 在staged上将所有文件移出缓存区, 在单个文件上将单个文件移出缓存区
* `U` 将所有文件移出缓存区
* `cc` 或 `:Gcommit` 用于提交暂存区中的文件
* `dd` 或 `:Gdiffsplit` 会打开两个水平分割窗口, 显示当前文件的diff信息
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

## Others
| git                  | fugitive          | action                                                   |
|----------------------|-------------------|----------------------------------------------------------|
| `:Git add %`         | `:Gwrite`         | Stage current file to the index                          |
| `:Git checkout %`    | `:Gread`          | Revert current file to last checked in version           |
| `:Git rm --cached %` | `:GDelete`        | Delete the current file and the corresponding Vim buffer |
|                      | `:GRemove`        | Like `:GDelete`, but keep the empty buffer around        |
| `:Git mv % {dest}`   | `:GMove {dest}`   | Rename the current file and the corresponding Vim buffer |
|                      | `:GRename {dest}` | Like `:GMove` but operates relative to the parent dir    |

* `Gpush`
* `Gclog` 使用quickfix列表显示git log
* `Gllog` 使用locallist信息显示git log
* `Gvdiffsplit` 使用垂直分割的窗口显示diff信息
