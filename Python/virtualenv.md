# Virtualenv

* `pip install virtualenv` 安装virtualenv
* `virtualenv <env_name>` 创建虚拟环境，会在当前目录下创建名为env_name的文件夹
* `virtualenv -p <python_path> <env_name>` 创建虚拟环境，使用指定的python解释器
* `source <env_name>/bin/activate` 激活env_name环境
* `deactivate` 退出虚拟环境
* `pip freeze --local > requirements.txt` 记录当前虚拟环境下的package和版本
* `rm -rf <env_name>` 删除env_name对应的文件夹即可删除该虚拟环境
