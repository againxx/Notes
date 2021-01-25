# Swap

## 普通容器的swap
* 普通的容器swap时并不会真正拷贝成员, 而是交换内部的data指针, 所以代价是常数量级
* swap后的绑定到元素的指针、引用和迭代器等仍然有效, 但是以及指向另外一个容器中的元素了
* 普通容器的内存都是分配在堆上的, 可以直接交换指针

```cpp
std::vector<int> vec1{1, 2, 3, 4, 5};
std::vector<int> vec2{6, 7, 8, 9, 10};

auto cit = std::cbegin(vec1);
for (int i = 0; i < 5; ++i) {
    std::cout << *cit++ << '\n';
    if (i == 2) {
        std::swap(vec1, vec2);
    }
}

if (cit == std::cend(vec2))
    std::cout << "Point to another vector" << '\n';

// 1 2 3 4 5
// Point to another vector
```

## string的swap
* swap后string的绑定到元素的指针、引用和迭代器等完全失效
    - 实际测试时发现当待交换的string长度较小时, 结果类似array
    - 当待交换的string长度较大时, 结果类似vector
    - 由于具有不确定性, 最好还是避免使用交换后的指针等
* 是否是因为small string optimization
    - small string optimization是指当string长度小于一定阈值时(vs中是16), 将string存储在栈上而不是堆上
    - 注意直接初始化的小string似乎并没有存储在栈上

```cpp
int a = 1;
auto b = new int(5);
std::string str1 = "hello";
std::string str2 = "hello world 1234";
std::string str3('a', 5);
std::cout << &a << '\n';
std::cout << static_cast<void*>(str1.data()) << '\n';
std::cout << b << '\n';
std::cout << static_cast<void*>(str2.data()) << '\n';
std::cout << static_cast<void*>(str3.data()) << '\n';

// 0x7fff348057e4
// 0x7fff34805800
// 0x555c5a79ce70
// 0x555c5a79ce90
// 0x555c5a79ceb0

```

## array swap
* array的swap会真正交换成员, 即调用拷贝赋值运算符, 所以代价和array中的元素数量成正比
* swap后array的绑定到元素的指针、引用和迭代器等仍然有效, 但是值已经和另外一个array中的元素互换了
* 可能的原因是因为array的内存是分配在栈上的, 不方便直接交换指针

```cpp
std::array<int, 5> arr1{1, 2, 3, 4, 5};
std::array<int, 5> arr2{6, 7, 8, 9, 10};

auto cit = std::cbegin(arr1);
for (int i = 0; i < 5; ++i) {
    std::cout << *cit++ << '\n';
    if (i == 2) {
        std::swap(arr1, arr2);
    }
}

// 1 2 3 9 10
```
