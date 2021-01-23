# Stack Unwinding
* **栈展开**: 指的是当内层函数抛出异常而没有被catch住的时候, 异常会一层层上抛, 从而导致栈上的局部对象依次销毁的过程
* 之所以叫栈展开是因为, 需要将压入栈中的栈帧一个个弹出来寻找catch语句, 在这个过程中栈里的数据被逐渐**展开**了

## Example
```cpp
class Obj
{
public:
    Obj()
    {
        std::cout << "Constructor" << '\n';
    }
    ~Obj()
    {
        std::cout << "Destructor" << '\n';
    }
};

void foo()
{
    Obj obj;
    throw std::runtime_error("Oh no");
}

int main()
{
    try
    {
        foo();
    }
    catch (std::runtime_error err)
    {
        std::cout << err.what() << '\n';
    }
    return 0;
}

// The local obj will be destroyed before the exception is caught
// Constructor
// Destructor
// Oh no
```
