# String

![String Memory Layout](https://gitee.com/againxx/image-storage/raw/master/images/string_layout.png =750x)
* In order to be compatible with c string, the `end()` iterator points to the `\0`

## Use string in interface
* Use `const char*` for easy string manipulation, which can save unnecessary string construction
* Use `const string& / string_view` for read only strings
* Use `string` for string will be changed inside the implementation
* Use `string&` for returning modified strings

## String View
* String view is a light weight immutable string data type, that **does not** own the content (like `&str` in Rust)
* Conversion from `std::string` / `constexpr char*` is O(1)
* Normally used as **pass by value** parameter in function

```cpp
// light weight struct
struct string_view {
    const char* data;
    std::size_t length;
};
```

### Advantages
* Most interfaces remain the same as `std::string`
    - `operator[]`
    - `back`
    - `at`
    - `data`
    - `find`
    - `substr` (O(1) since no need for creating substring copy)
* Extra interfaces
    - `remove_prefix`
    - `remove_suffix`

### Limitations
* Does not support appending, concatenation
* Lifetime issue
    - Make sure data is not mutated during the lifetime of `string_view`

```cpp
std::string s{"abcdefg"};
std::string_view sv = s;
s = "123";
std::cout << sv << '\n'; // undefined behavior
```
