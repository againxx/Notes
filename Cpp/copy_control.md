# Copy Control

Copy Control由五中特殊的成员函数控制:
1. 拷贝构造函数(copy constructor)
2. 拷贝赋值运算符(copy-assignment operator)
3. 移动构造函数(move constructor)
4. 移动赋值运算符(move-assignment operator)
5. 析构函数(destructor)

缺失时, 编译器会自动定义缺失的操作.

**析构函数一般与拷贝构造函数和赋值操作符同时出现**

因为如果自定义了析构函数, 类中必然出现了指针类型的成员(否则默认析构函数即可),
这时需要通过自定义拷贝构造函数和赋值操作符来防止**浅拷贝**问题
