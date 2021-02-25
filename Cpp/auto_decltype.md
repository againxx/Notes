# Auto & Decltype

## Auto
* `auto` 以引用对象的类型作为推导类型, 而不包含引用本身, 所以`&`符号需要单独写出来
* `auto` 会去掉顶层const, 但保留底层const, 顶层const需要明确指出

## Decltype
* 变量的`decltype`永远是变量的类型, 即引用类型的变量`decltype`之后得到引用类型
* 表达式的`decltype`由表达式结果是左值还是右值决定, 左值表达式的类型是引用, 右值表达式不是
    - 因而`decltype((var))`会得到引用类型, 括号运算符使得变量变成了表达式, 而变量作为表达式是左值

## Difference
* `auto` 会实际计算表达式的值来为变量进行初始化, 同时推断类型
* `auto` 会去掉顶层const
* `auto` 会去掉reference
* `auto` 倾向于保留尽可能简单的类型(核心类型), 而去掉了引用和const这些附属修饰
* `decltype` 仅仅推断类型而不实际计算表达式
* `decltype` 不会去掉顶层const

## Example
```cpp
int i = 0, &r = 1;
auto a = r; // int

const int ci = i, &cr = ci;
auto b = ci;        // int
auto c = cr;        // int
auto d = &i;        // int*
auto e = &ci;       // const int*
const auto f = ci;  // const int
auto &g = ci;       // const int&
auto &h = 42;       // error, h will be deduced to int&
const auto &j = 42; // const int&
```

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

auto increment(int& a) // the deduced type is int
{
    a++;
    return a;
}

decltype(auto) increment(int& a) // the deduced type is int&
{
    a++;
    return a;
}
```
