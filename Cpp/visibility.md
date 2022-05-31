# Visibility

## Why should we use C++ visibility?
Put simply, it hides most of the ELF symbols which would have previously and unnecessarily been public
* It very substantially improves load times of the DSO
* It lets the optimizer produce better code
    - PLT indirections through *Global Offset Table* can be completely avoided
        - This substantially avoiding pipeline stalls on modern processors
        - When you declare something defined outside the current compilation unit, GCC cannot know if that symbol resides
        inside or outside the DSO, so GCC must assume the worst and route everything through the GOT
    - When most of the symbols are bound locally, they can be safely elided completely
* It reduces the size of the DSO by 5-20%
    - ELF's exported symbol table format is quite a space hog since the mangled symbol names are normally quite long
    - C++ templates spew out a huge amount of symbols
* Much lower chance of symbol collision, which solves the **Global Symbol Interpose** problem

## How to use C++ visibility support?
* In header files, wherever you want an interface or API made public outside the current DSO, place
`__attribute__ ((visibility ("default")))` in struct, class, and function declarations you wish to make public
* Then alter the make system to pass `-fvisibility=hidden` to each call of GCC compiling a source file

```cpp
#if defined(_WIN32) || defined(__CYGWIN__)
#define OPEN3D_DLL_IMPORT __declspec(dllimport)
#define OPEN3D_DLL_EXPORT __declspec(dllexport)
#define OPEN3D_DLL_LOCAL
#else
#define OPEN3D_DLL_IMPORT [[gnu::visibility("default")]]
#define OPEN3D_DLL_EXPORT [[gnu::visibility("default")]]
#define OPEN3D_DLL_LOCAL [[gnu::visibility("hidden")]]
#endif

#ifdef OPEN3D_STATIC
#define OPEN3D_API
#define OPEN3D_LOCAL
#else
#define OPEN3D_LOCAL OPEN3D_DLL_LOCAL
#if defined(OPEN3D_ENABLE_DLL_EXPORTS)
#define OPEN3D_API OPEN3D_DLL_EXPORT
#else
#define OPEN3D_API OPEN3D_DLL_IMPORT
#endif
#endif

class OPEN3D_API SomeClass
{
    int c_;
    OPEN3D_LOCAL void privateMethod(); // only for use within this DSO
public:
    SomeClass(int c) : c_(c) {}
    static void foo(int a);
};
```

* Use `xxx_DLL_LOCAL` for every local symbols is cumbersome, this is why `-fvisibility` was added.
* With `-fvisibility=hidden`, you are telling GCC that every declaration not explicitly marked with a visibility attribute has a hidden visibility
* Even for classes marked as visible (exported from the DSO), you may still want to mark private members as hidden, so that optimal code will be
produced when calling them from within this DSO
* `-fvisibility-inlines-hidden` causes all inlined class member functions to have hidden visibility


## Reference
* [Visibility - GCC Wiki](https://gcc.gnu.org/wiki/Visibility)
* 程序员的自我修养 7.6.2节
