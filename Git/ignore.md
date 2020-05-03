# Ignore

* 子目录也可以拥有`.gitignore`文件，并且比全局`.gitignore`文件拥有更高的优先级
* 在子目录`.gitignore`文件里，可以通过`!<pattern>`来否定之前的ignore
* `.gitignore`文件中可以使用`#`来注释
* `git ls-files --others --ignored --exclude-standard` 展现目前git ignore的文件
