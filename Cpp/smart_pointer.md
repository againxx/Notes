# Smart Pointer

[Original Version](https://www.internalpointers.com/post/beginner-s-look-smart-pointers-modern-c)

## Basics of Dynamic Memory
* 动态分配的对象是默认初始化的（内置类型或组合类型的值是未定义的）
* `new (nothrow)` 如果分配失败返回空指针 (参考C++ Primer 12.1.2)
* `new T[N]` require to be deleted with `delete[]`, using the wrong form results in undefined behavior
* 使用动态内存的三个原因:
    1. 程序不知道自己需要使用多少对象
    2. 程序不知道所需对象的准确类型
    3. 程序需要在多个对象间共享数据

## Three Types of Smart Pointer

Defined in `<memory>` header

* `std::unique_ptr`: exclusive version
* `std::shared_ptr`: several `shared_ptr`s may own the same resource and an internal counter keeps track of them
* `std::weak_ptr`: like a `std::shared_ptr`, but it doesn't increment the counter

## std::unique_ptr
A `std::unique_ptr` owns of the object it points to and no other smart pointers can point to it

Created like this:
```cpp
std::unique_ptr<Type> p(new Type);
// For example
std::unique_ptr<int>    p1(new int);
std::unique_ptr<int[]>  p2(new int[50]);
std::unique_ptr<Object> p3(new Object("Lamp"));
// With the help of the special function std::make_unique
std::unique_ptr<int>    p1 = std::make_unique<int>();
std::unique_ptr<int[]>  p2 = std::make_unique<int[]>(50);
std::unique_ptr<Object> p3 = std::make_unique<Object>("Lamp");
```
There can be at most one `std::unique_ptr` pointing at any one resource. You can't have multiple references to its dynamic data.
```cpp
void compute(std::unique_ptr<int[]> p) { ... } 

int main()
{
    std::unique_ptr<int[]> ptr = std::make_unique<int[]>(1024);
    std::unique_ptr<int[]> ptr_copy = ptr; // ERROR! Copy is not allowed
    compute(ptr);  // ERROR! `ptr` is passed by copy, and copy is not allowed
}
```
### unique_ptr和shared_ptr都支持的操作
|                        |                                            |
|------------------------|--------------------------------------------|
| shared_ptr<T> sp       | 空智能指针                                 |
| unique_ptr<T> up       | 可以指向类型为T的对象                      |
| make_unique<T>(*args*) | 返回一个unique_ptr, 使用*args*初始化此对象 |
| make_shared<T>(*args*) | 返回一个shared_ptr, 使用*args*初始化此对象 |
| p                      | 将p作为条件判断, 若p指向一个对象, 则为true |
| *p                     | 解引用p, 获得它指向的对象                  |
| p->mem                 | 等价于(*p).mem                             |
| p.get()                | 返回p中保存的指针                          |
| swap(p, q)             | 交换p和q中的指针                           |
| p.swap(q)              |                                            |

## std::shared_ptr
`std::shared_ptr` has the technique called **reference counting**, and allows for multiple references.
When the very last one is destroyed the counter goes to zero and the data will be deallocated.

A `std::shared_ptr` is constructed like this:
```cpp
std::shared_ptr<Type> p(new Type);
// For example:
std::shared_ptr<int>    p1(new int);
std::shared_ptr<Object> p2(new Object("Lamp"));
// Using by the special function std::make_shared
std::shared_ptr<int>    p1 = std::make_shared<int>();
std::shared_ptr<Object> p2 = std::make_shared<Object>("Lamp");
```
### Issue with arrays
Until C++17 there is no easy way to build a `std::shared_ptr` holding an array.
Prior to C++17 this smart pointer always calls `delete` by default (and not `delete[]`) on its resource:

You can create a workaround by using a **custom deleter**.
```cpp
std::shared_ptr<int[]> p2(new int[16], [] (int* i) { 
delete[] i; // Custom delete
});
// Or using default_delete provider by std
std::shared_ptr<bool[]> tempPtr(new bool[voxelNum], std::default_delete<bool[]>());
```
Unfortunately there's no way to do this when using `std::make_shared`.

### shared_ptr独有的操作
|                        |                                                                                    |
|------------------------|------------------------------------------------------------------------------------|
| shared_ptr<T> p(sp)    | p是shared_ptr sp的拷贝; 递增sp中的计数器. sp中的指针必须能转换为T*                 |
| p = sp                 | p和sp都是shared_ptr, 所保存的指针必须能相互转换, 递减p的引用计数, 递增sp的引用计数 |
| p.unique()             | 若p.use_count()为1返回true, 否则为false                                            |
| p.use_count()          | 返回与p共享对象的智能指针数; 可能很慢, 主要用于调试                                |
| shared_ptr<T> p(q)     | p管理内置指针q所指向的对象; q必须指向new分配的内存, 且能转换T*                     |
| shared_ptr<T> p(u)     | p从unique_ptr u那里接管了对象的所有权; 将u置空                                     |
| shared_ptr<T> p(q, d)  | p接管内置指针q所指对象, p将使用可调用对象d来代替delete                             |
| shared_ptr<T> p(sp, d) | p是shared_ptr sp的拷贝, p将使用可调用对象d来代替delete                             |
| p.reset()              | 减少p的计数器, 将p置空                                                             |
| p.reset(q)             | 减少p的计数器, 令p指向内置指针q                                                    |
| p.reset(q, d)          | 减少p的计数器, 令p指向内置指针q, 使用可调用对象d来代替delete                       |

**注意: 只有通过拷贝创建的shared_ptr之间, 才会有联动的计数器, 用同一个内置指针(包括通过get()获得的)初始化两个shared_ptr是危险的行为**

### Circular References
For example, I'm writing a game where a player has another player as companion.
```cpp
struct Player
{
  std::shared_ptr<Player> companion;
  ~Player() { std::cout << "~Player\n"; }
};

int main()
{
  std::shared_ptr<Player> jasmine = std::make_shared<Player>();
  std::shared_ptr<Player> albert  = std::make_shared<Player>();

  jasmine->companion = albert; // (1)
  albert->companion  = jasmine; // (2)
}
```
When `jasmine` goes out of scope at the end of the program, its destructor can't cleanup the memory:
there is still one smart pointer pointing at `jasmine-data`, that is `albert->companion`.
At this point the program just quits without freeing memory.

## std::weak_ptr
`std::weak_ptr` is basically a `std::shared_ptr` that doesn't increase the reference count.
It is defined as a smart pointer that holds a **non-owning reference**, or a **weak reference**,
to an object that is managed by another `std::shared_ptr`.

You can only create `std::weak_ptr` out of a `std::shared_ptr` or another `std::weak_ptr`
```cpp
// p_weak1 and p_weak2 point to the same dynamic data owned by p_shared,
// but the reference counter doesn't grow.
std::shared_ptr<int> p = std::make_shared<int>(100);
std::weak_ptr<int> wp1(p);
std::weak_ptr<int> wp2(wp1);
```
由于对象可能不存在，不能使用`weak_ptr`直接访问对象，必须调用`lock`。此函数检查`weak_ptr`指向的对象是否存在。
如果存在，`lock`返回一个指向共享对象的`shared_ptr`，与其他任何`shared_ptr`类似，只要此`shared_ptr`存在，
它所指向的底层对象也会一直存在。
```cpp
if (std::shared_ptr<int> np = wp1.lock()) { // np不为空则条件成立
    // 在if中，np与p共享对象
}
```

### weak_ptr支持的操作 
|                   |                                                                            |
|-------------------|----------------------------------------------------------------------------|
| weak_ptr<T> w     | 空weak_ptr可以指向类型为T的对象                                            |
| weak_ptr<T> w(sp) | 与shared_ptr sp指向相同对象的weak_ptr. T必须能转换为sp指向的类型           |
| w = p             | p可以是一个shared_ptr或weak_ptr. w与p共享对象                              |
| w.reset()         | 将w置为空                                                                  |
| w.use_count()     | 与w共享对象的shared_ptr的数量                                              |
| w.expired()       | 若w.use_count()为0, 返回true, 否则false                                    |
| w.lock()          | 若expired为true, 返回一个空shared_ptr; 否则返回一个指向w的对象的shared_ptr |

### weak_ptr解决循环引用
`std::weak_ptr` can also used to break a **circular reference**.
Back to Player example above and change the member variable from `std::shared_ptr<Player>` companion to `std::weak_ptr<Player>` companion.
In this case we used a std::weak_ptr to dissolve the entangled ownership. The actual dynamically-allocated data stays in the main body,
while each Player has now a **weak reference** to it.

## Advantage of make_unique and make_shared
1. Let us forget about the `new` keyword
2. Make your code safe against exceptions

Consider following example
```cpp
void function(std::unique_ptr<A>(new A()), std::unique_ptr<B>(new B())) { ... }
```
Suppose that `new A()` succeeds, but `new B()` throws an exception: you catch it to resume the normal execution of your program.
Unfortunately, the C++ standard does not require that object A gets destroyed and its memory deallocated:
memory silently leaks and there's no way to clean it up. By wrapping A and B into std::make_uniques you are sure the leak will not occur:
```cpp
void function(std::make_unique<A>(), std::make_unique<B>()) { ... }
```

The point is `std::make_unique<A>` and `std::make_unique<B>` are now temporary objects,
and cleanup of temporary objects is correctly specified in the C++ standard.
