# Homebrew

## Basic Usage
* `brew search <string>` 查找可安装的包
* `brew install <package_name>`
* `brew uninstall <package_name>`
* `brew info <package_name>` 查看包的信息, 同时会列出依赖信息
* `brew list` 列出当前安装的所有包
* `brew outdated` 列出所有过时的包
* `brew update` 获取最新版的brew和formulae
* `brew upgrade` 更新所有过时的包
* `brew cleanup` 清除一些包的旧版本, 因为brew更新包时不会自动清除旧的版本
* `brew doctor` 出现问题时进行一些自我诊断, 可以忽略warnings
* `brew tap <repo_name>` tap a new formula repository, 类似apt的ppa源
* `brew deps --installed --tree` 以树形图输出所有安装包的依赖关系

## Formulae
Command line software

## Casks
An extension to homebrew which contains some GUI applications

* `brew cask install <package_name>` 还有很多类似cask开头的命令
