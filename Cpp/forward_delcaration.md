# Forward Declaration & Incomplete Type

## Forward Declaration
仅纯粹声明函数、类或模板而暂时不定义它
```cpp
class Screen;   // Screen类的声明
```

## Incomplete Type
在类被前向声明之后定义之前, 他是一个**不完全类型** (incomplete type)

* Incomplete type只能在有限的情况下使用:
    - 定义指向这种类型的指针或引用
    - 声明(但不能定义)以不完全类型作为参数或返回类型的函数

* 不能使用的情况:
    - 创建它的对象
    - 引用或者指针访问其成员
    - 声明数据成员为该种类类型

**一个类的成员类型不能是该类自己, 但是可以是指向它自身类型的引用或指针, 因为一旦一个类的名字出现后, 它就被认为是声明过了(但尚未定义)**
```cpp
class Link_screen {
    Screen window;
    Link_screen *next;
    Link_screen *prev;
}
```

## Advantages
* 前置声明能节省编译时间, 多余的`#include`会迫使编译器展开更多的文件, 处理更多的输入
* 前置声明能节省不必要的重新编译时间, `#include`使`.cpp`因为头文件的无关改动而被重新编译多次

## Disadvantages
* 前置声明隐藏了依赖关系, 头文件改动时, 用户的代码会跳过必要的重新编译过程
* 前置声明可能会被库的后续更该所破坏. 前置声明或模板有时会妨碍头文件开发者变动其API, 例如扩大形参类型, 加个自带默认参数的模板形参.
* 前置声明来自namespace `std::` 的symbol时, 其行为未定义
* 前置声明了不少来自头文件的symbol时, 比单单一行`include`冗长
* 仅仅为了能前置声明而重构代码 (比如用指针成员代替对象成员) 会使代码变得更慢更复杂.
* 很难判断什么时候该用前置声明, 什么时候该用`include`. 极端情况下, 用前置声明代替`include`甚至都会暗暗地改变代码的含义:
```cpp
// b.h:
struct B {};
struct D : B {};

// good_user.cc:
#include "b.h"
void f(B*);
void f(void*);
void test(D* x) { f(x); }  // calls f(B*)

struct B;
struct D;
void f(B*);
void f(void*);
void test(D* x) { f(x); }  // calls f(void*)
```
