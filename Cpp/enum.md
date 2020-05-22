# Enumeration

* **枚举类型** (enumeration) 将一组整型常量组织在一起
* 每个枚举类型定义了一种新的类型
* 枚举类型属于字面值常量类型

参考C++ Primer 19.3

## 限定作用域的枚举类型 (scoped enumeration)
枚举成员的名字遵循常规的作用域准则, 在枚举类型的作用域外是不可访问的.
```cpp
enum class open_modes {input, output, append};
// 等价于
enum struct open_modes {input, output, append};
```

* 默认情况下, 枚举值从0开始, 依次加1.
* 可以专门为一个或几个枚举成员指定值, 如果没有显式初始值, 当前枚举成员的值等于之前枚举成员的值加1

```cpp
enum class intTypes {
    charTyp = 8, shortTyp = 16, intTyp = 16, // 枚举值不一定唯一
    longTyp = 32, long_longTyp = 64
}
```

## 不限定作用域的枚举类型 (unscoped enumeratino)
枚举成员的作用域与枚举类型本身的作用域相同.
```cpp
enum color {red, yellow, green} // 不限定作用域的枚举类型, 省略class
// 未命名的, 不限定作用域的枚举类型, 只能在定义该enum时定义它的对象
enum {floatPrec = 6, doublePrec = 10, double_doublePrec = 10} eobj1, eobj2;

// 错误: 重复定义了枚举成员
enum stoplight {red, yellow, green};

// 正确: 枚举成员被隐藏了
enum class peppers {red, yellow, green};
```
