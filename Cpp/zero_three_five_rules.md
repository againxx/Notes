# The Rule of Zero/Three/Five

## Speical member functions
* Destructor
* Copy constructor
* Copy assignment operator
* Move constructor
* Move assignment operator

## Implicit definitions of these functions
> The implementation will implicitly declare these member functions for some class types when the program does not explicitly declare them but are used.

> The implicitly-defined copy constructor for a non-union class X performs a memberwise copy of its subobjects.

> The implicitly-defined copy assignment operator for a non-union class X performs memberwise copy assignment of its subobjects.

## Problem with implicit definitions
根据RAII思想, 如果一个类负责管理一块资源, 并且需要在析构函数里手动释放资源. 则memberwise拷贝的默认拷贝构造函数和默认拷贝赋值函数,
将会造成资源在多个对象间共享, 相互却并不知道. 从而可能出现以下问题:
1. 对一个对象a的改变会反应在另一个对象b上面
2. 一旦对象b被销毁, 它共享资源的对象a将会操作无效资源(野指针)
3. 当对象a销毁时, 释放已经无效的资源(double free)是未定义行为
4. 默认拷贝赋值操作没有考虑先释放已有资源, 从而造成资源泄漏

## Reference
[c++ - What is The Rule of Three? - Stack Overflow](https://stackoverflow.com/questions/4172722/what-is-the-rule-of-three)
