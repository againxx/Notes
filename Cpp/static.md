# Static

## Static variable in global scope
定义在所有函数和类外的static变量只对当前编译单元(.cpp文件)可见, 其他编译单元无法使用该static变量

## Static variable in class
申明在类内的static变量为该类所有实例公共所有, 需要在类外再定义一遍(此时不需要加static)

## Static method in class
static method只能访问类的static变量, 原因是其没有类实例的指针(this)作为隐式参数传入, 类似python的classmethod

## Static variable in local scope
* 可以从作用域和生命周期两个视角来看待静态局部变量
    - 静态变量意味着该变量始终存在, 第一次定义时分配, 之后便不再重复分配了
    - 但是局部变量意味着该变量只能在申明它的作用域中访问
* 静态局部变量可以用来简化单例模式的代码

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
