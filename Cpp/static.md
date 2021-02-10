# Static

## Static variable in global scope
* 定义在所有函数和类外的static变量只对当前编译单元(.cpp文件)可见, 其他编译单元无法使用该static变量
* 全局static函数也只在该编译单元中可见
* 注意这种静态声明的做法其实是从C语言继承而来的, 现在已经被C++标准取消了, 现在的做法是使用**未命名命名空间**

## Static variable in class
申明在类内的static变量为该类所有实例公共所有, 需要在类外再定义一遍(此时不需要加static)
    - 因为类中所列的成员变量其实都只是声明
    - 真正的定义应该发生在该类对象定义的时候(猜测)
    - 而static变量属于类而不属于对象, 所以不会随着任何一个对象的定义而定义, 因而只能单独在类外定义
    - `static const / constexpr int` 变量虽然能提供类内初时值, 但是只能用作值替换, 而无法取地址
    - 如果类内提供了初时值, 则定义时不能再指定初时值了

## Static method in class
* static method只能访问类的static变量, 原因是其没有类实例的指针(this)作为隐式参数传入, 类似python的classmethod
* 在类外定义static method时不能重复static关键字

## Static variable in local scope
* 可以从作用域和生命周期两个视角来看待静态局部变量
    - 静态变量意味着该变量始终存在, 第一次定义时分配, 之后便不再重复分配了
    - 但是局部变量意味着该变量只能在申明它的作用域中访问
* 静态局部变量可以用来简化单例模式的代码
* 或者帮助确认静态变量的初始化顺序, 因为C++没法保证全局static变量的初始化顺序, 所以如果全局static变量之间有相互依赖关系,
  可以考虑将其变成局部static变量

```cpp
class Singleton
{
public:
    static Singleton& get()
    {
        static Singleton instance;
        return instance;
    }
};
```

## Cost of using static
There was an enhancement to C++11 guranteeing that the initialization of static variables happens in a thread safe manner, so
    - The complier has to check whether the static variable has already been constructed
    - If not, it will perform a lock and construct the variable for us
    - So, every time we run a function with a static variable, there will be a overload for checking its state

```cpp
struct C
{
    static const std::string &magic_static()
    {
        static const std::string s = "bob";
        return s;
    }
    // class initialization
    const std::string &s = magic_static();

    const std::string &magic_static_ref()
    {
        return s;
    }
};

// This is more expansive
C::magic_static().size();
// Than this
C c;
c.magic_static_ref().size();
```

## Reference
[C++ Weekly - Ep 2 Cost of Using Statics - YouTube](https://www.youtube.com/watch?v=B3WWsKFePiM&list=PLs3KjaCtOwSZ2tbuV1hx8Xz-rFZTan2J1&index=2)
