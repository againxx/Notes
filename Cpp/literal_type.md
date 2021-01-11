# Literal Type
* 比较简单, 值显而易见, 容易得到的类型
* 用于申明constexpr时用到的类型

包含:
* 算术类型
* 引用
* 指针
* 字面值常量类
* 枚举类型(enumeration)

## 字面值常量类 (literal class type)
C++ primer 7.5.6

* 数据成员都是字面值类型的聚合类
* 如果不是聚合类, 需要满足:
    - 数据成员必须是字面值类型
    - 类必须至少含有一个constexpr构造函数
    - 如果一个数据成员含有类内初时值, 则内置类型成员的初时值必须是一条常量表达式;
      或者如果成员属于某种类类型, 则初时值必须使用该成员自己的constexpr构造函数
    - 类必须使用析构函数的默认定义

### constexpr构造函数
* constexpr构造函数可以申明成`=default`
* 否则constexpr构造函数必须符合构造函数的要求(不能包含返回语句)
* 同时又必须符合constexpr函数的要求(它能拥有的唯一可执行语句就是返回语句)
* 综合上面两点, constexpr构造函数的函数体一般是空的
* constexpr构造函数必须初始化所有数据成员

```cpp
class Debug {
public:
    constexpr Debug(bool b = true) : hw(b), io(b), other(b) { }
    constexpr Debug(bool h, bool i, bool o) : hw(h), io(i), other(o) { }
    constexpr bool any() { return hw || io || other; }
    void set_hw (bool b) { hw = b; }
    void set_io (bool b) { io = b; }
    void set_other (bool b) { other = b; }

private:
    bool hw;    // hardware error
    bool io;    // io error
    bool other; // other error
};

constexpr Debug io_sub(false, true, false); // debug io
if constexpr (io_sub.any())
    std::cerr << "print appropriate error message" << std::endl;

constexpr Debug prod(false); // no debug
if constexpr (prod.any())
    std::cerr << "print an error message" << std::endl;
```
