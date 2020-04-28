# Pip

| commands                            | description                                         |
|-------------------------------------|-----------------------------------------------------|
| `pip help [<command>]`              | 查看全部或具体某个command的帮助                     |
| `pip search <package>`              | 搜索package                                         |
| `pip list`                          | 列出所有安装的package                               |
| `pip list -o, --outdated`           | 列出可以更新的package                               |
| `pip install -U, --upgrade`         | 更新package                                         |
| `pip install -r <requirements.txt>` | 安装requirements.txt中指定的package以及对应版本     |
| `pip uninstall <package>`           | 删除package                                         |
| `pip freeze`                        | 输出所有package以及对应的版本号, 可用于`install -r` |
| `pip freeze > requirements.txt`     | 提供给别人你的package环境, 配合`install -r`使用     |
