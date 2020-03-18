# Basic Commands

## Config & Help
* 安装完成后，第一步需要设置名字和邮箱  
```shell
git config --global user.name "<your name>"
git config --global user.email "<your email>"
```
* `git config --list` 能列出当前所有的设置
* `git help <verb>` 或 `git <verb> --help` 来列出对应动作的帮助信息

## Initialize repository
* `git init` 初始化本地版本库
* `git clone <url> [<where to clone>]` 克隆已有的版本库
* `git clone --depth <n> <url> [<where to clone>]` 克隆已有的版本库，并截取最近n次commits

## Three basic concepts
Git has three basic concepts or area to store information
* __Working directory__: untracked files
* __Staging area__: 
* __Repository__:

**Trasition:**  
Working directory -> Staging area
* `git add <file>` 添加文件
* `git add -A` 添加所有文件

Staging area -> Working directory
* `git reset <file>` 不缓存文件
* `git reset` 不缓存所有文件

Staging area -> Repository
* `git commit -m <message>` 提交更新

