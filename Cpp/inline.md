# Inline
* The compiler is free to decide inline or not
* Inline means to allow an exception to the one definition rule, so you can put functions etc. in a header file and not get linker errors.
* Inline functions are usually defined in header file, since inlining action is taken by compiler during compiling time (some may during linking time)

## Pros & Cons
Pros:
* 免除函数调用成本
* 编译器最优化机制通常被设计用来浓缩那些"不含函数调用"的代码

Cons:
* 增加你的object code大小, 从而增加换页行为(paging), 降低指令高速缓存装置的击中率(instruction cache hit rate)
* inline函数无法伴随library的升级而升级, 用到library中inline函数的程序都需要重新编译而不是重新链接
* 大部分调试器对inline函数束手无策

## Implicitly & Explicitly
* Implicitly: define function in class definition
* Explicitly: use `inline` keyword before function definition

## Inline constructor / deconstructor is not a good idea?
该说法来自Effective C++ 条款30: 透彻了解inlining的里里外外
* 作者原义是派生类中inline构造函数和析构函数可能带来的成本
    - 因为派生类的构造函数需要构造基类和自身的成员属性, 并处理异常
    - 从而引入若干额外的代码, 使得看似空的构造函数并不空空如也
* 关键还是得自己综合考虑

## Reference
[Why are inline constructors and destructors not a good idea in C++? - Stack Overflow](https://stackoverflow.com/questions/7138234/why-are-inline-constructors-and-destructors-not-a-good-idea-in-c)
