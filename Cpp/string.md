# String

![String Memory Layout](https://gitee.com/againxx/image-storage/raw/master/images/string_layout.png =750x)
* In order to be compatible with c string, the `end()` iterator points to the `\0`

## Use string in interface
* Use `const char*` for easy string manipulation, which can save unnecessary string construction
* Use `const string& / string_view` for read only strings
* Use `string` for string will be changed inside the implementation
* Use `string&` for returning modified strings
