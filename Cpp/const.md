# Const

## 顶层const和底层const
* 只有指针才区分顶层const和底层const的概念
* 顶层const: 对象本身是常量
* 底层const: 所指对象是常量
* 引用只有底层const, 无论是写在类型名前还是后
* 其余对象只有顶层const

```cpp
int i = 0;
int *const p1 = &i;       // 不能改变p1的值, 顶层const
const int ci = 42;        // 不能改变ci的值, 顶层const
const int *p2 = &ci;      // 允许改变p2的值, 但是不能改变p2所指对象的值, 底层const
const int *const p3 = p2; // 靠右的是顶层const, 靠左的是底层const
const int &r = ci;        // 用于申明引用的const都是底层const
int const &r = ci;        // 等价于上述申明
int *p = p3;              // 不能用有底层const的指针去初始化一个没有底层const的指针
int &r = ci;              // 底层const的引用同理
```

## 基于const的重载
C++ primer 7.3.2

原因：非const版本的函数对常量对象是不可用的，需要定义一个const版本来供常量对象调用。
另一方面，虽然非常量对象能调用非const版本和const版本，但是非const版本是更好的匹配。

```cpp
class Screen
{
public:
    Screen &diplay(std::ostream &os) { do_display(os); return *this; }
    const Screen &diplay(std::ostream &os) const { do_display(os); return *this; }
private:
    void do_display(std::ostream &os) const { os << contents; }
}
```
当一个成员调用另外一个成员时, `this`指针在其中隐式传递。当`display`的非const版本调用`do_display`时，它的`this`指针将隐式地
从非const指针转换成const指针。`display`函数各自返回解引用`this`指针所得的对象，在非const版本中，this指向一个非const对象，
因此display返回一个普通的引用；而const成员函数则返回一个const引用。

在某个对象上调用`display`时，该对象是否为const决定了调用`display`的哪个版本
```cpp
Screen myScreen(5, 3);
const Screen blank(5, 3);
myScreen.set('#').display(cout); // 调用非const版本
blank.display(cout);             // 调用const版本
```
