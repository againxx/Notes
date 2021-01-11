# Explicit
如果一个类的构造函数只接受一个实参(可以有多个形参, 但是其余形参拥有默认值), 则它实际上定义了转换为此类类型的隐式转换机制
也被称为转换构造函数(converting constructor)

## Example
```cpp
class Book
{
public:
    Book(std::string bookName, double bookPrice = 0.0)
    {
        name = bookName;
        price = bookPrice;
    }

    // If remove the const, a temporary variable cannot be passed into this function
    void testFunction(const Book & otherBook)
    {
        std::cout << name << " " << otherBook.name << std::endl;
    }

    std::string name;
    double price;
};

int main(int argc, char *argv[])
{
    Book book1("c++ primier");
    Book book2("pragmatic programmer");
    std::string rlName = "rl introduction";
    book1.testFunction(rlName);
    // Only one implicit converting is allowed
    book2.testFunction("rl introduction"); // invalid, two converting: const char * -> string -> Book
    // These two are ok
    book2.testFunction(std::string("rl introduction"));
    book2.testFunction(Book("rl introduction"));
    return 0;
}
```

## Explicit keyword
我们可以通过将构造函数申明成explicit, 来加以阻止隐式转换
```cpp
class Book
{
    // Only used before single parameter constructor
    explicit Book(std::string bookName, double bookPrice = 0.0);
};

// explicit keyword is only allowed in class declaration
Book::Book(std::string bookName, double bookPrice)
{
    name = bookName;
    price = bookPrice;
}
```
