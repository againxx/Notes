# Auto & Decltype

## Decltype
* 变量的`decltype`永远是变量的类型, 即引用类型的变量`decltype`之后得到引用类型
* 表达式的`decltype`由表达式结果是左值还是右值决定, 左值表达式的类型是引用, 右值表达式不是
    - 因而`decltype((var))`会得到引用类型, 括号运算符使得变量变成了表达式, 而变量作为表达式是左值

## Difference
* `auto` 会实际计算表达式的值来为变量进行初始化, 同时推断类型
* `decltype` 仅仅推断类型而不实际计算表达式
* `auto` 会去掉顶层const
* `decltype` 不会去掉顶层const

## Example
```cpp
int a = 3;
auto c1 = a;
decltype(a) c2 = a;
decltype((a)) c3 = a;

const int d = 5;
auto f1 = d; // auto会去掉顶层const
decltype(d) f2 = d;

std::cout << typeid(c1).name() << '\n'; // int
std::cout << typeid(c2).name() << '\n'; // int
std::cout << typeid(c3).name() << '\n'; // int&
std::cout << typeid(f1).name() << '\n'; // int
std::cout << typeid(f2).name() << '\n'; // const int
```
