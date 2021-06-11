# Singleton Pattern

> Ensure a class only has one instance, and provide a global point of access to it.

## Advantage
* Singleton may not be necessary in C++, the same functionality can be achieved by global variable and functions encapsulated in a namespace
* But using a class can still organize things well (global variables and functions)

## Possible Implementations
```cpp
class Singleton {
public:
    // note that explicitly deleted copy constructor and copy assignment operator
    // will indicate implicitly deleted move constructor and move assignment operator
    // so this class doesn't have all four copy control members
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton& getInstance() {
        return instance;
    }
private:
    Singleton() {}

    float member = 0.0F;

    static Singleton instance;
}

Singleton::Singleton instance;
```

Use method local static variable instead
```cpp
class Random {
public:
    Random(const Random&) = delete;
    Random& operator=(const Random&) = delete;

    static Random& getInstance() {
        static Random instance;
        return instance;
    }

    // use a static method to simplify interface
    static float getFloat() { return getInstance().getFloatImpl(); }
private:
    Random() {}

    float getFloatImpl();
}
```
