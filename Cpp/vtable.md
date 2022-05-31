# Vtable

## Cue
* What's the concept of dynamic dispatch?
* Why we need virtual table?
* Who will have virtual table?
* How can we refer to virtual table?
* What's the disadvantages of virtual table method?
* Why should the destructor of base class be virtual?

## Dynamic Dispatch
Virtual table is mainly used to support dynamic dispatch
* Static dispatch (early binding): the compiler knows which routine to execute during compilation time (find the address for the called function)
* Dynamic dispatch (late binding): the compiler has to find the right virtual function definition at runtime
* The virtual table method is a popular implementation of dynamic dispatch

## Virtual Table Implementation
* For every class that contains virtual functions, the compiler constructs a virtual table
* The vtable contains entries for each virtual function accessible by the class and stores a pointer to its definition, which includes
    - virtual functions declared in the class itself, e.g. `C::bar()`
    - virtual functions inherited from the base class, e.g.  `C::qux()`
* vtable exists at class level, meaning there exists a single vtable per class, and is shared by all instances
* We can use `g++ -fdump-class-hierarchy` to examine virtual table and vpointer

![vtable example](http://images.againxx.cn/vtables.png =750x)

## Vpointer
* The class having vtable will have an extra member **vpointer**, which points to the virtual table
    - This will also increase the class size, and can be checked will `sizeof(class_type)`
* When a call to a virtual function on an object is performed, the vpointer of that object is used to find the corresponding vtable of the class
* Next the function name is used as index to the vtable to find the correct routine to be executed

![vpointer example](http://images.againxx.cn/vpointer.png =750x)

## Reference
[Understandig Virtual Tables in C++ | Pablo Arias](https://pabloariasal.github.io/2017/06/10/understanding-virtual-tables/)
