# Git Status

* `git status` 标准版状态显示, 会有不少说明和命令提示
* `git status -s / git status --short` 简短版状态显示
    - `??` 新添加的未跟踪文件
    - `A` 新添加到暂存区的文件
    - `M` 修改过的文件
    - 输出中有两栏, 左栏是暂存区的状态, 右栏是工作区的状态
* `git status -sb` 同上, 增加了本地分支和跟踪分支的信息
