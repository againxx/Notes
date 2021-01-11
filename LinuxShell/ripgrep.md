# Ripgrep

```shell
rg <pattern> <file_name>
```

* 如果file_name缺省, 则会自动递归搜索整个当前目录, 不需要像`grep`一样需要`-r`参数
* `-n` 显示行号
* `-t` 只搜索指定类型, 例如只搜索cpp文件`-tcpp`
* `-T` 不搜索指定类型
