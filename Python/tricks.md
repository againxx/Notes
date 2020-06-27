# Python Tricks

* `python -i <file>` 进入交互模式, 可以调用file中定义的函数、变量等
* `python -m <module>` 将模块以main的方式执行
* `{key: value for item in iterable if some_condition}` dict comprehension
* 使用下划线来分割数字, 从而增加可读性, `10_000_000_000`
* 使用`context manager`来管理需要手动释放的资源
* 使用`enumerate`同时遍历列表项和下标, 可以使用`enumerate(list, start=1)`来调整起始下标
* 使用`zip`来同时遍历多个lists
* 在unpack的时候, 可以在某个变量前面加*, 使它接受所有剩余的值
* 使用`setattr`和`getattr`来动态的设置对象的属性, 这两个函数可以接受变量作为参数, 而不一定是字符串
* 使用`getpass`模块中的`getpass`来读取密码
* 使用`help()`查看module的帮助文档
* 使用`dir()`查看某个object的所有可用的方法和属性
