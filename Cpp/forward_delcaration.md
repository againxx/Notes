# Forward Declaration & Incomplete Type

## Forward Declaration
仅声明函数或类而暂时不定义它
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
