# Translation Unit and Linkage

## Declaration vs Definition

> A _declaration_ introduces (or reintroduces) a name into the program, along with enough information to later associate the name with a definition

> A _definition_ introduces a name and provides all the information needed to create it

> One Definition Rule: a symbol can only be defined once

* If the name represents a variable, a definition explicitly creates storage and initializes it
* A function definition consists of the signature plus the function body
* A class definition consists of the class name followed by a block that lists all class members
    - The bodies of member functions may optionally be defined separately in another file
    - Since the class can be created without knowing its member functions' definition, the compiler only needs to know how many space it should allocates for an class object

## Translation Units
* A program consists of one or more _translation units_
* A translation unit consists of an implementation file and all the headers that it includes directly or indirectly
* Each translation unit is compiled independently by the compiler
* Violations of the ODR rule typically show up as linker errors
* By adding _include guards_ around the header contents, you ensure that the names a header **declares** are only declared once for each translation unit

## Linkage
* In some cases, it may be necessary to declare a global variable or class in a `.cpp` file. In those cases, you need a way to tell the compiler and linker what kind of _linkage_ the name has.
* The type of linkage specifies whether the name of the object is visible only in one file, or in all files. ( **visibility** )
* The concept of linkage applies only to global names
* Non-const global variables and free functions by default have _external linkage_, they're visible from any translation unit in the program, and can only appear once
* A symbol with _internal linkage_ or _no linkage_ is visible only within the translation unit in which it's declared
    - When a name has internal linkage, the same name may exist in another translation unit
    - Variables declared within class definitions or function bodies have no linkage
* You can force a global name to have internal linkage by explicitly declaring it as `static`. In this context, `static` means something different than when applied to local variables
    - The following objects have internal linkage by default:
        - `const` objects
        - `constexpr` objects
        - `typedef` objects
        - `static` objects in namespace scope
