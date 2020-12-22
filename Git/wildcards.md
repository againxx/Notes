# Git Wildcards

* git命令可以使用glob模式, 但是git有自己的文件模式扩展匹配方式,不需要shell来帮忙扩展, 故通配符`*` 前要加`\`
* `git rm log/\*.log` 删除log/目录下扩展名为.log的所有文件
