# Interface
An interface in Java is a specification of method prototypes
* All the methods of the interface are **public** and **abstract**
* Interfaces were first introduced in Java to work around the lack of multiple inheritance

## Purpose
* **Provides communication**: specify how you want the methods and fields of a particular type
* **Multiple inheritance**: Java doesn’t support multiple inheritance, using interfaces you can achieve multiple inheritance
* **Abstraction**: the user will have the information on what the object dose instead of how it does it
* **Loose coupling**: 

## Example
```java
interface MyInterface{
   public void display();
   public void setName(String name);
   public void setAge(int age);
}
```

## Interface in C++
* C++ supports multiple inheritance, and so a special type isn't needed.
* An abstract base class with no non-abstract (pure virtual) methods is functionally equivalent to a C#/Java interface.

```cpp
class IDemo
{
public:
    // destructor need to be virtual instead of pure virtual
    virtual ~IDemo() = default;
    virtual void OverrideMe() = 0;
};

class Parent
{
public:
    virtual ~Parent();
};

class Child : public Parent, public IDemo
{
public:
    virtual void OverrideMe()
    {
        //do stuff
    }
};
```
