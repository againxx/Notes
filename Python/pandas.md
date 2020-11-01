# Pandas
## Cues
* What's the difference between numpy and pandas?
* What's the two key classes in pandas?
* How to get and set elements in pandas?

## DataFrame
* DataFrame可以理解为每列类型不同的二维数组, 其中
    - 行用index引用(默认是0开始的整数)
    - 列用column name引用

* Difference between **Numpy** and **Pandas**
    - All the elements of a Numpy array have the same type
    - Columns in DataFrame can have different types

* DataFrame的构建
    - `read_csv` 从csv读入DataFrame
    - `to_csv` 将DataFrame写入csv文件
    - `pd.DataFrame(dict)` 从一个dict初始化DataFrame, dict的key是column name, value是每一行的值

* DataFrame的属性
    - `df.shape`
    - `df.columns`

* DataFrame的方法
    - `df["<column_name>"].value_counts()` 统计某一个column的不同值的数量
    - `df.head(<num>) / df.tail(<num>)` 列出开头/结尾的num行(默认5行)
    - `df.describe()` 显示一个快速的统计结果
    - `df.rename(columns={<old_column_name>: <new_column_name>})` 修改某些column的名字

## Series

## Indexes
* 行默认的index为从0开始的整数
* `df.set_index("<column_name>")` 使用某一个column的值作为index, 默认是非inplace的, 可以通过参数`inplace=True`来指定
* `df.index` 列出当前使用的index
* `df.reset_index()` 重置index为从0开始的整数
* `read_csv(..., index_col='<column_name>')` 在读取DateFrame的时候, 设置index为某一列

## Indexer
* `df.iloc` 用整数索引rows或者columns, 索引多项时需要用list of integer(方括号扩起来的整数); 或者用slice, 这个时候就不需要方括号了
* `df.loc` 用index或者key索引rows或者columns, 同样可以用字符串来slice columns, 和整数一样, 此时slice的末端是包含的
* `df.at` 更快的访问单个元素

### SettingwithCopyWarning
由于pandas内部调用了numpy, 当对一个DataFrame索引时, 无法确定返回的子数据是view还是copy. 所以对链接索引赋值(chained assignment)时,
其实是对一个中间临时变量赋值, 无法确定是否会修改原始DataFrame, 因而会有警告.

避免方法有
* 使用`loc`或者`iloc`同时取出想要修改的行和列, 从而避免链接索引
* 显式的使用`.copy()`方法指定返回copy而不是view
* 使用`pd.set_option('mode.chained_assignment', None)`关闭警告, 也可以使用`with pd.option_context('mode.chained_assignment, None'):`来局部关闭警告

## Filtering
* 通过逻辑运算符`&`, `|` 和 `~`来组合筛选行的mask
* 再通过`loc`获取筛选后的数据

## Apply a Function to the Data
* Functions used on Series
    - `apply(<function>)`, 对Series中的每一个元素应用一个函数
    - `map({<old_value>: <new_value>})`, values that are not listed in dict will be turned into `NaN`
    - `replace({<old_value>: <new_value>}>)`, values that are not listed in dict will keep unchanged
* Functions used on DataFrame
    - `apply(<function>)`, 对DataFrame中的每一个Series应用一个函数
    - `applymap(<function>)`, 对DataFrame中的每一个元素应用一个函数

## Options
* `pd.set_option('display.max_columns', 85)` 对Jupyter notebook有效, ipython好像无效
* `pd.set_option('display.max_rows', 85)`

## Reference
* [SettingwithCopyWarning: How to Fix This Warning in Pandas – Dataquest](https://www.dataquest.io/blog/settingwithcopywarning/)
