# PImpl

"Pointer to implementation" or "pImpl" is a C++ programming technique that
removes implementation details of a class from its object representation by placing them in a separate class, accessed through an opaque pointer:

## Explanation
* private data members participate in its object representation, affecting size and layout
* private member functions participate in overload resolution (which takes place before member access checking)

## Advantages
* Optimize compilation times
    - Changes in implementation do not require components that only depend on interface to be recompiled
* Completely hide the implementation when distributing a pre-compiled library
    - Pimpl can hide private member declarations as well, otherwise, you need to include them in public header files
* Switch class implementations transparently to user of the class

## Alternatives
* inline implementation: private members and public members are members of the same class (normal way)
* pure abstract class (OOP factory): users obtain a unique pointer to a lightweight or abstract base class,
  the implementation details are in the derived class that overrides its virtual member functions

## Reference
[PImpl - cppreference.com](https://en.cppreference.com/w/cpp/language/pimpl)
