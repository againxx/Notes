# Constexpr
const expression是指值不会改变, 并在编译期就能得到计算结果的表达式

包含:
* 字面值常量
* 用常量表达式初始化的const对象

## Advantages
* Runtime efficiency by moving things from runtime to compile time
    - No execution time
    - Minimal executable footprint (less binary code)
* Errors found at compile or link time
* Clearer code by using fewer magic numbers since we can use more const expression to compute these magic numbers
* Less cross-platform pain by reducing steps in tool chain
* No synchronization concerns
    - Don't have to deal with any races with a const container
* Like template metaprogramming
    - But uses familiar C++ syntax
    - Therefore easier to maintain

## constexpr关键字

### constexpr变量
* C++11允许将变量声明为 **constexpr** 类型, 以便由编译器来验证变量的值是否为常量表达式
* 申明为constexpr的对象一定是常量, 必须用常量表达式来初始化
```cpp
constexpr int mf = 20;          // 20是常量表达式
constexpr int limit = mf + 1;   // mf + 1是常量表达式
constexpr int sz = size();      // 只有当size()函数是一个constexpr函数时才正确
```

### constexpr指针
* constexpr指针的初时值必须是nullptr或者0, 或者是存储于某个固定地址中的对象
    - 局部static变量
    - 全局变量
* constexpr把它所定义的对象置为顶层const, 因而constexpr指针可以指向非常量的对象
```cpp
// i, j须定义于函数体外
int j = 0;
constexpr int i = 42;
constexpr int *p1 = &j; // p1是常量指针, 指向整数j
constexpr const int *p2 = &i; // p2是常量指针, 指向整形常量i
const int constexpr *p3 = &i; // p3的定义等价于p2, 各清晰的表示了constexpr设置的是顶层const
```
