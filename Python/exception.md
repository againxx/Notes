# Exception

处理错误的几种方式:
* 错误码: 用一个整数表示调用结果, 比如`open()`函数, 缺点是调用者需要用大量的代码判断是否出错
* try...except...finally...机制

## try机制
* 将可能出错的代码放在`try`中
* 如果抛出对应的错误, 则会被`except`捕获, 执行`except`中的语句, `try`中剩下的语句不会被执行
* 如果有`finally`块的话, 则一定会被执行, 无论是否出错

```python
try:
    print("try...")
    r = 10 / 0
    print("result: ", r)
except ZeroDivisionError as e:
    print("except: ", e)
finally:
    print("finally...")
```

* 可以有多个`except`块, 用来捕获不同的错误
* 可以加上一个`else`块, 当没有错误发生时, 自动执行`else`块中的内容
```python
try:
    print("try...")
    r = 10 / int('a')
    print("result: ", r)
except ValueError as e:
    print("ValueError: ", e)
except ZeroDivisionError as e:
    print("ZeroDivisionError: ", e)
else:
    print("no error!")
finally:
    print("finally...")
```

* 使用`except`时, 父类会将子类的错误也捕获
```python
try:
    foo()
except ValueError as e:
    print("ValueError")
except UnicodeError as e:
    print("UnicodeError") # this error will never be catched
```

## raise
* `raise`不带参数就会把当前的错误原样抛出
* 也可以在`except`中通过`raise`将一种类型的错误装换成另一种类型
