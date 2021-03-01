# Cast

`cast-name<type>(expression)`

## static_cast
* 任何具有明确定义的类型转换, 只要不包含底层const, 都可以使用`static_cast`
* 根据Effective C++条款三的说法, 添加底层const的时候也可以使用`static_cast`
* 但是为了表示清晰, 个人还是使用`const_cast`
* 当把一个较大的算术类型赋给较小的类型时, `static_cast`比较有用, 可以抑制编译器的warning
* `static_cast`的另外一个作用是找回存在 void* 中的指针

## dynamic_cast

## const_cast
* `const_cast`只能用来改变底层const
* 常用于在非const成员函数中调用const成员函数

```cpp
std::string& shorterString(std::string& str1, std::string& str2) {
    return const_cast<std::string&>(shorterString(
                const_cast<const std::string&>(str1),
                const_cast<const std::string&>(str2)));
}

// example from effective c++
char& operator[](std::size_t position) {
    return const_cast<char&>(
        static_cast<const TextBlock&>(*this)
            [position]
    );
}
```

## reinterpret_cast
* 为运算对象的位模式提供较低层次上的重新解释
* 可用于将多个数据压缩到一个对象中
