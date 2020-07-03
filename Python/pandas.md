# Pandas

## DataFrame
* DataFrame的行用index引用(默认是0开始的整数), 列用column name引用
* `read_csv` 从csv读入DataFrame
* `pd.DataFrame(dict)` 从一个dict初始化DataFrame
* `df.shape`
* `df.columns`
* `df.iloc` 用整数索引rows或者columns, 索引多项时需要用list of integer; 或者用slice, 这个时候就不需要方括号了
* `df.loc` 用key或者index索引rows或者columns, 同样可以用字符串来slice columns, 和整数一样, 此时slice的末端是包含的
* `df["<column_name>"].value_counts()` 统计某一个column的不同值的数量

## Series

## Indexes
* 行默认的index为从0开始的整数
* `df.set_index("<column_name>")` 使用某一个column的值作为index, 默认是非inplace的, 可以通过参数`inplace=True`来指定

## Options
* `pd.set_option('display.max_columns', 85)` 对Jupyter notebook有效, ipython好像无效
* `pd.set_option('display.max_rows', 85)`
