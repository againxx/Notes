# Anaconda

* `conda list` 结果中py结尾的package都是python的包，在`pip list` 中同样会显示
* `conda create --name, -n <env_name> <package_list>` 创建一个虚拟环境，可以跟一个以上的初始package
* `conda install <package_name>=<package_version>` 安装指定版本的package
* `conda activate <env_name>` 激活环境
* `conda deactivate` 退出环境
* `conda env list` 列出当前所创建的所有环境
* `conda env remove --name, -n <env_name>` 删除环境
* `conda remove --name, -n <env_name> --all` 删除环境
* `conda remove [-n <env_name>] <package_list>` 删除指定环境的指定package
