# Enumeration

* **枚举类型** (enumeration) 将一组 **整型常量** 组织在一起
* 每个枚举类型定义了一种新的类型
* 枚举类型属于 **字面值常量** 类型
* 要想初始化或者为enum对象赋值, 必须使用该类型的一个枚举成员或者该类型的另一个对象

参考C++ Primer 19.3

## 限定作用域的枚举类型 (scoped enumeration, C++11)
枚举成员的名字遵循常规的作用域准则, 在枚举类型的作用域外是不可访问的.
```cpp
// 定义
enum class open_modes {input, output, append};
// 等价于
enum struct open_modes {input, output, append};

// 错误: 2不属于类型open_modes
open_modes om = 2;
// 正确: input是open_modes的一个枚举成员
om = open_modes::input;
```

* 默认情况下, 枚举值从0开始, 依次加1.
* 可以专门为一个或几个枚举成员指定值, 如果没有显式初始值, 当前枚举成员的值等于之前枚举成员的值加1
* 枚举值不一定唯一

```cpp
enum class intTypes {
    charTyp = 8, shortTyp = 16, intTyp = 16, // 枚举值不一定唯一
    longTyp = 32, long_longTyp = 64
}
```

* 枚举成员是const, 初始化枚举成员时提供的初始值必须是常量表达式
* 每个枚举成员本身就是一条常量表达式, 可以在任何需要常量表达式的地方使用枚举成员
```cpp
constexpr intTypes charbits = intTypes::charTyp

// 将enum作为switch语句的表达式, 将枚举值作为case标签
switch (charbits) {
    case intTypes::charTyp:
        break;
    case intTypes::shortTyp:
        break;
    case intTypes::intTyp:
        break;
    case intTypes::longTyp:
        break;
}

// 将枚举类型作为一个非类型模板形参使用?

// 在类的定义中初始化枚举类型的静态数据成员
class IntArray {
private:
    static constexpr intTypes dtype = intTypes::longTyp;
}
```

## 不限定作用域的枚举类型 (unscoped enumeration, C语言)
枚举成员的作用域与枚举类型本身的作用域相同.
```cpp
// 不限定作用域的枚举类型, 省略class
enum color {red, yellow, green}
// 未命名的, 不限定作用域的枚举类型, 只能在定义该enum时定义它的对象
enum {floatPrec = 6, doublePrec = 10, double_doublePrec = 10} eobj1, eobj2;

// 错误: 重复定义了枚举成员
enum stoplight {red, yellow, green};

// 正确: 枚举成员被隐藏了
enum class peppers {red, yellow, green};

// 正确: 不限定作用域的枚举类型的枚举成员位于有效的作用域中
color eyes = green;

// 错误: peppers的枚举成员不在有效的作用域中
// colors::green在有效的作用域中, 但是类型错误
peppers p = green;

// 正确: 允许显示地访问枚举成员
color hair = color::red;

// 正确: 使用peppers的red
peppers p2 = peppers::red;
```

要想初始化一个enum对象, 必须使用该enum类型的另一个对象或者它的一个枚举成员
```cpp
enum Tokens {INLINE = 128, VIRTUAL = 129};
void ff(Tokens);
void ff(int);

Tokens curTok = INLINE;
ff(128);    // 精确匹配ff(int)
ff(INLINE); // 精确匹配ff(Tokens)
ff(curTok)  // 精确匹配ff(Tokens)
```

不限定作用域的枚举类型的对象或枚举成员自动地转换成整型, 因此可以在任何需要整型值的地方使用它们.
不限定作用域的枚举类型传递给整型实参时, 会提提升成int或更大的整型, 但是永远不会提升成unsigned char.
```cpp
// 正确: 不限定作用域的枚举类型的枚举成员隐式地转换成int
int i = color::red;
// 错误: 限定作用域的枚举类型不会进行隐式转换
int j = peppers::red;

void newf(unsigned char);
void newf(int);
unsigned char uc = VIRTUAL;
newf(VIRTUAL); // 调用newf(int)
newf(uc);      // 调用newf(unsigned char)
```

## Miscellaneous
### 指定enum的大小
* 可以在enum的名字后加上冒号以及想在该enum中使用的类型
* 如果未指定enum的潜在类型, 限定作用域的enum成员类型默认是int, 不限定作用域的enum成员不存在默认类型, 但是其类型足够大使其能容纳枚举值

```cpp
enum intValues : unsigned long long {
    charTyp = 255, intTyp = 65535,
    long_longTyp = 18446744073709551615ULL
}
```

### 枚举类型的前置声明
* enum的前置声明(无论隐式地还是显示地)必须指定其成员的大小
* enum的所有声明和定义中成员的大小必须一致
```cpp
enum intValues : unsigned long long; // 不限定作用域的, 必须指定成员类型
enum class open_modes; // 限定作用域的可以使用默认成员类型int
 // 错误: 已声明为不限定作用域的
enum class intValues;
// 错误: intValues已经被声明为unsigned long long
enum intValues : long;
```
