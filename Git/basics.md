# Basic Commands

## Config & Help
* 安装完成后，第一步需要设置名字和邮箱  
```shell
git config --global user.name "<your name>"
git config --global user.email "<your email>"
```
* `git config --list` 能列出当前所有的设置
* `git config --global http.proxy "<http://url:port>"` 来设置http代理
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

Working directory -> Null
* `git restore <file>, git checkout -- <file>` 丢弃工作区的修改

Working directory -> Staging area
* `git add <file>` 添加文件
* `git add -A` 添加所有文件

Staging area -> Working directory
* `git reset <file>` 不缓存文件
* `git reset` 不缓存所有文件

Staging area -> Repository
* `git commit -m <message>` 提交更新
* `git log` 查看提交历史

## Remote repository
* `git remote add origin git@github.com:againxx/***.git` 将一个已有的本地仓库和远程仓库关联，其中origin是远程仓库在本地的名字，是Git的默认叫法
* `git push -u origin master` 将本地master推送到远程master，并将两者关联，之后只用`git push origin master`即可
* `git remote -v` 列出远程仓库的信息
* `git remote set-url origin git@github.com:againxx/***.git` 将远程库改为SSH连接方式, 每次不需要输入密码
* `git remote set-url origin https://github.com/againxx/***.git` 将远程库改为HTTPS连接方式, 每次需要输入密码
* `git pull origin master` 多人合作时应记得在push之前pull
