# Types

## 14 kinds of types
1. void (only has one element)
2. integral
3. floating point
4. nullptr (only has one element)
5. class
6. array
7. pointer
8. rvalue reference
9. lvalue reference
10. union
11. enum
12. function
13. member object pointer
13. member function pointer

![type hierarchy](https://gitee.com/againxx/image-storage/raw/master/images/20210810094936.png =750x)
* there are more integral types now

## Type traits
> A type traits is a (templated) struct, and the member variable(s) and/or member types of the struct give you information about the type that it is templated on

### Why should we use type traits?
1. Writing generic algorithms
2. Restrict templates (use `enable_if`)
3. Provide **optimized** version of generic code for some types, first analyze code at compile-time and based on that analysis to choose the optional version
    - `std::vector` will check if type T is movable and non-except when allocating new memory, otherwise it has to copy the old elements instead (strong exception guarantee)
    - Further more, `std::vector` can check trivial copyable to decide whether to use `memcpy` directly without calling constructor, which is even faster
        - Internally, C functions like `memcmp`, `memset`, `memcpy`, or `memmove` are used

## Reference
* [CppCon 2015:Marshall Clow “Type Traits - what are they and why should I use them?" - YouTube](https://www.youtube.com/watch?v=VvbTP_k_Df4)
* [Type-Traits: Performance Matters - ModernesCpp.com](https://www.modernescpp.com/index.php/type-traits-performance-matters)
