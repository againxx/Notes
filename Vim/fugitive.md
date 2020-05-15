# Fugitive

## Gstatus / G
* `<C-n> / <C-p>` 上下移动到修改过的文件, 回车可打开该文件
* `-` 将文件移入或移出暂存区
* `s` 在unstaged上将所有文件移入缓存区, 在单个文件上将单个文件移入缓存区
* `u` 在staged上将所有文件移出缓存区, 在单个文件上将单个文件移出缓存区
* `cc` 或 `:Gcommit` 用于提交暂存区中的文件
* `dd` 或 `:Gdiffsplit` 
* `g?` 显示命令帮助

## Others
* `Gpush`
* `Gclog` 使用quickfix列表显示git log
* `Gllog` 使用locallist信息显示git log
