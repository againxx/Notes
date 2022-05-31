# Concept

## Why do we need concepts?
Before C++20, we have two different ways to think about functions and classes. Functions and classes can be defined on specific types or generic types.
* Defined on specific types can be too cumbersome to cover some many types. To avoid that burden, **type conversion** provide some conveniences, but may incur unexpected results
    - Narrowing conversion
    - Integral promotion
* Defining too generic codes only relies on template parameter names and documentations to regulate the type requirements
    - Unconstrained templates are C++'s **compile-time duck types**
```cpp
template<typename RandomIt>
void sort(RandomIt first, RandomIt last);
```

## The advantages of concepts:
* Requirements for templates are part of the interface.
* The overloading of functions or specialization of class templates can be based on concepts.
* We get an improved error message because the compiler compares the requirements of the template parameter with the actual template arguments.
* You can use predefined concepts or define your own.
* The usage of auto and concepts if unified. Instead of auto, you can use a concept.
* If a function declaration use a concepts, it automatically becomes a function template. Writing function template is, therefore, as easy as writing a function.

## Three usage ways
```cpp
// Requires clause
template<typename Cont>
    requires Sortable<Cont>
void sort(Cont& container);

// Trailing requires clause
template<typename Cont>
void sort(Cont& container) requires Sortable<Cont>;

// Constrained template parameters
template<Sortable Cont>
void sort(Cont& container);
```

## Overloading
Depending on the iterator, the implementation of `std::advance` can use pointer arithmetic or just go _n_ times further. These two cases have different computational complexity
```cpp
template<InputIterator I>
void advance(I& iter, int n) {...} // implementation for iterator that only fulfill InputIterator

template<BidirectionalIterator I>
void advance(I& iter, int n) {...} // implementation for iterator that fulfill BidirectionalIterator

template<RandomAccessIterator I>
void advance(I& iter, int n) {...} // implementation for iterator that fulfill RandomAccessIterator

// usage
std::vector<int> vec{1, 2, 3, 4, 5, 6, 7, 8, 9};
auto vecIt = vec.begin();
std::advance(vecIt, 5);     // use RandomAccessIterator version

std::list<int> lst{1, 2, 3, 4, 5, 6, 7, 8, 9};
auto lstIt = lst.begin();
std::advance(lstIt, 5);     // use BidirectionalIterator version

std::forward_list<int> forw{1, 2, 3, 4, 5, 6, 7, 8, 9};
auto forwIt = forw.begin();
std::advance(forwIt, 5);    // use InputIterator version
```

## Unification with auto
Concepts can be used where `auto` is usable

## Difference between concepts and types
* A type
    - Specifies the set of operations that can be applied to an object
        - Implicitly and explicitly
        - Relies on function declarations and language rules
    - But also specifies how an object is laid out in memory

* A concept
    - Specifies the set of operation that can be applied to an object
        - Implicitly and explicitly
        - Relies on use patterns
            - reflecting function declarations and language rules
    - Says **nothing** about layout of the object

## C++ concepts vs Haskell type classes
* In Haskell, a type has to be an instance of a type class. In C++20, a type has to fulfill the requirements of a concept.
* Concepts can be used on non-type arguments of templates.
* Concepts add no run-time costs.

## Reference
* [CppCon 2018: Bjarne Stroustrup “Concepts: The Future of Generic Programming (the future is here)” - YouTube](https://www.youtube.com/watch?v=HddFGPTAmtU&t=1888s)
