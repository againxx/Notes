# Extern

The `extern` keyword extends the visibility of variables and functions

## Extern for Functions
When a function is declared or defined, the extern keyword is **implicitly** assumed, when we write
```c
int foo(int arg1, char arg2);
// The compiler treats it as:
extern int foo(int arg1, char arg2);
```

* The function can be used (called) anywhere in any of the files of the whole program, provided those files contain a declaration of the function.
* With the declaration of the function in place, the compiler knows the definition of the function exists somewhere else and it goes ahead and compiles the file

## Extern for Variables
We need to explicitly include the `extern` keyword when we want to declare variables without defining them
```c
extern int var;
// extern int var = 0; same as definition
// main(void) means main doesn't take any arguments
// in C func() can take any arguments
// in C++ func() is the same as func(void)
int main(void) {
    var = 10;
    return 0;
}
```
* This program throws an error in the compilation(during the linking phase) because var is declared but not defined anywhere.

## Summary
1. A declaration can be done any number of times but definition only once.
2. the extern keyword is used to extend the visibility of variables/functions.
3. Since functions are visible throughout the program by default, the use of extern is not needed in function declarations or definitions. Its use is implicit.
4. When extern is used with a variable, it’s only declared, not defined.
5. As an exception, when an extern variable is declared with initialization, it is taken as the definition of the variable as well.

## Reference
[Understanding "extern" keyword in C - GeeksforGeeks](https://www.geeksforgeeks.org/understanding-extern-keyword-in-c/)
