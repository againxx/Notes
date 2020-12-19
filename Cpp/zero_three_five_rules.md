# The Rule of Zero/Three/Five
C++中管理资源的类需要同时实现几个特殊的成员函数, 这个法则被称为0/3/5法则

## Speical member functions (copy control)
* Destructor
* Copy constructor
* Copy-assignment operator
* Move constructor
* Move-assignment operator

## Implicit definitions of these functions
> The implementation will implicitly declare these member functions for some class types when the program does not explicitly declare them but are used.

> The implicitly-defined copy constructor for a non-union class X performs a memberwise copy of its subobjects.

> The implicitly-defined copy assignment operator for a non-union class X performs memberwise copy assignment of its subobjects.

> The implicitly-defined destructor is always empty.

## Problem with implicit definitions
根据RAII思想, 如果一个类负责管理一块资源, 并且需要在析构函数里手动释放资源. 则memberwise拷贝的默认拷贝构造函数和默认拷贝赋值函数,
将会造成资源在多个对象间共享, 相互却并不知道. 从而可能出现以下问题:
1. 对一个对象a的改变会反应在另一个对象b上面
2. 一旦对象b被销毁, 它共享资源的对象a将会操作无效资源(野指针)
3. 当对象a销毁时, 释放已经无效的资源(double free)是未定义行为
4. 默认拷贝赋值操作没有考虑先释放已有资源, 从而造成资源泄漏

## A bad example that disobey the rule
```cpp
class person
{
    char* name;
    int age;
public:
    person(const char * the_name, int the_age)
    {
        name = new char[strlen(the_name) + 1];
        strcpy(name, the_name);
        age = the_age;
    }
    
    ~person()
    {
        delete [] name;
    }
};
```

## Explicit definitions of speical functions
```cpp
// 1. copy constructor
person(const person & that)
{
    name = new char[strlen(that.name) + ];
    strcpy(name, that.name);
    age = that.age;
}

// 2. copy assignment operator
person & operator=(const person & that)
{
    if (this != &that)
    {
        delete [] name;
        // This is a dangerous point in the flow of execution!
        // We have temporarily invalidated the class invariants,
        // and the next statement might throw an exception,
        // leaving the object in an invalid state :(
        name = new char[strlen(that.name) + 1];
        strcpy(name, that.name);
        age = that.age;
    }
    return *this;
}

// 2. copy assignment operator in an exception safety way
// another way is to use copy-and-swap idiom
person & operator=(const person & that)
{
    char* local_name = new char[strlen(that.name) + 1];
    // If the above statement throws,
    // the object is still in the same state as before.
    // None of the following statements will throw an exception :)
    strcpy(local_name, that.name);
    delete [] name;
    name = local_name;
    age = that.age;
    return *this;
}
```

## Noncopyable resources
Some resources cannot or should not be copied, such as file handles or mutexes, just declare them as deleted
```cpp
person(const person & that) = delete;
person & operator=(const person & that) = delete;
```

## The Rule of Zero / Three / Five
> If you need to explicitly declare either the destructor, copy constructor, copy assignment operator yourself,
> you probably need to explicitly declare all three of them

> The rule of five adds another two functions, move constructor and move assignment operator

> The rule of zero states that you are allowed to not write any of the special member functions when creating your class

## Reference
[c++ - What is The Rule of Three? - Stack Overflow](https://stackoverflow.com/questions/4172722/what-is-the-rule-of-three)
