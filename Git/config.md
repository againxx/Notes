# Git Config

Git有三个级别的配置文件, 每个级别会覆盖上一级别的配置
1. `--system`: 位于`/etc/gitconfig`, 包含系统上每一个用户及他们仓库的通用配置
2. `--global`: 位于`~/.gitconfig`或`~/.config/git/config`, 只针对当前用户的所有仓库
3. `--local`: 位于当前仓库的`.git/config`, 针对该仓库, 默认情况下用的就是它

* `git config --list` 能列出当前所有的设置
* `git config --list --show-origin` 查看所有的配置以及它们所在的文件
* `git config <key>` 检查某一项配置
* `git config --show-origin <key>` 查询某一项配置, 并告诉你哪一个配置文件最后设置了该值
