# Initialization

## 默认初始化 (default initialized)

如果定义变量时未指定初始值, 则变量被默认初始化(default initialized)

* 内置类型:
    * 定义于任何函数体之外的变量被初始化为0
    * 定义于函数体之内的变量不被初始化(uninitialized), 该变量的值是未定义的
        - 主要是为了兼容C, 减少额外初始化带来的效率降低
* 类类型:
    * 由是否由默认构造函数，以及默认构造函数的行为决定

### 默认初始化的情况
* 默认构造的std::array是非空的, 包含了和其大小一样多的元素, 这些元素默认初始化
* 动态分配的对象是默认初始化的
    - `new int / new std::string` 均为默认初始化
    - `new int() / new std::string()` 为值初始化
    - 对于定义了自己的构造函数的类类型(例如`std::string`), 默认初始化和值初始化其实没什么区别
    - 对于`int`这样的内置类型, 则差别很大
* 没有初时值的类数据成员将被默认初始化

## 值初始化 (value-initialized)

在标准库容器中, 如果初始化时只提供元素数量不提供初始值, 则会创建值初始化的元素初值, 并把它赋给容器中的元素。


这个初值由容器中对象的类型决定
* 内置类型
    * 初始值为0
* 类类型
    * 由类默认初始化。

### 值初始化的情况
* 如果对std::array进行列表初始化, 初始值的数目必须等于或小于array的大小, 如果初始值数目小于array的大小, 它们被用来初始array中靠前的元素, 所有剩余元素进行值初始化
* For **aggregate class**, when using list initialization, if the number of initial values less than the number of members, the remained members will be value-initialized

## 列表初始化 (list initialization)

* 无论是初始化对象还是某些时候为对象赋新值，都可以使用由花括号括起来的初始值
* 可以用花括号来值初始化内置对象
```cpp
// 以下4条语句等价
int units_sold = 0;
int units_sold = {0};
int units_sold(0);
int units_sold{0};
int units_sold{};
```
当用于内置类型变量时，如果使用列表初始化且初始值存在丢失信息的风险，则编译器将报错
```cpp
long double pi = 3.1415926536;
int a{pi}, b = {pi}; // 错误：转换未执行，因为存在丢失信息的风险
int c(ld), d = pi;   // 正确：转换执行，且确实丢失了部分值
```

## 直接初始化

## 拷贝初始化
何时发生:
* 用=定义变量时
* 将一个对象作为实参传递给一个非引用类型的形参
* 从一个返回类型非引用类型的函数返回一个对象
* 用花括号列表初始化一个数组中的元素或一个聚合类中的成员
* 初始化标准库容器或是调用其insert或push时

```cpp
std::string dots(10, '.'); // 直接初始化
std::string s(dots); // 直接初始化, 但是调用了拷贝构造函数
std::string s2 = dots; // 拷贝初始化, 也调用了拷贝构造函数
std::string null_book = "9-999-9999-9"; // 拷贝初始化, 但是没有调用拷贝构造函数, 因为编译器可以(但是不必须)跳过拷贝/移动构造函数
std::string null_book("9-999-9999-9"); // 被编译器改写, 但是拷贝/移动构造函数必须是存在且可访问的(例如, 不是private的)
```

## initializer_list
C++ primer 6.2.6节

处理可变数量实参的三种方法:
1. initializer_list: 处理实参类型相同的情况
2. 可变参数模板 (variadic template): 处理实参类型不同的情况
3. 省略符 (ellipsis parameter): 用于和C函数交互的接口程序

### initializer_list
定义在`<initializer_list>`头文件中

|                                       |                                                                                 |
|---------------------------------------|---------------------------------------------------------------------------------|
| `initializer_list<T> lst;`            | 默认初始化; T类型元素的空列表                                                   |
| `initializer_list<T> lst{a, b, c...}` | lst的元素数量和初始值一样多; lst的元素是对应初始版本的副本; 列表中的元素是const |
| `lst2(lst)`                           | 拷贝或赋值一个initializer_list对象不会拷贝列表中的元素;                         |
| `lst2 = lst`                          | 拷贝后, 原始列表和副本共享元素                                                  |
| `lst.size()`                          | 列表中的元素数量                                                                |
| `lst.begin()`                         | 返回指向lst中首元素的指针                                                       |
| `lst.end()`                           | 返回指向lst中尾元素下一位置的指针                                               |

**注意: 虽然返回的是const值, 却没有cbegin()和cend()方法**

* initializer_list对象中的元素永远是常量值, 无法改变
* 向initializer_list形参中传递一个值的序列, 必须把序列放在一对花括号内
* 含有initializer_list形参的函数也可以同时拥有其他形参
* initializer_list可以在参数列表的任意位置 (不必是最后一个)

```cpp
void error_msg(ErrCode e, initializer_list<string> il)
{
    cout << e.msg() << ": ";
    for (const auto &elem : il)
        cout << elem << " ";
    cout << endl;
    // 或用begin()和end()访问元素
    // for (auto beg = il.begin(); beg != il.end(); ++beg)
    //     cout << *beg << " ";
}

if (expected != actual)
    error_msg(ErrCode(42), {"functionX", expected, actual});
else
    error_msg(ErrCode(0), {"functionX", "okay"});
```

### 省略符形参
> 省略符形参应该仅仅用于C和C++通用的类型. 大多数类类型的对象在传递给省略符形参时都无法正确拷贝.

```cpp
// 省略符只能出现在形参列表最后
void foo(param_list, ...);
void foo(...);
```

## Reference
* [Copy elision - cppreference.com](https://en.cppreference.com/w/cpp/language/copy_elision)
