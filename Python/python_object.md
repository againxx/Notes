# Python Object

## id & type
* 可以用`id()`和`type()`函数来确认python中对象的地址和类型
* [-5, 256]区间内的整数值, bool对象, None对象, 较短的字符串对象(长度不超过20, 且仅由字母、下划线、数字组成),
共用相同的地址(即由相同的id)

## True & False
* 所有非零的数值都映射为True, 0, 0.0, 0j映射为False
* 所有空字符串, 空数组, 空列表, 空字典都映射为False
* `isinstance(True, int)`和`isinstance(False, int)` 为True
