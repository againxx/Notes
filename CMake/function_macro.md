# Function & Macro

* It's common to dereference nested variable in function
```cmake
function(print var)
    message("${var} = ${${var}}")
endfunction()
```

## Use arguments
* All following arguments will not include the function name, unlike bash `$0`
    * `ARGV` all arguments passed to function
    * `ARGN` all arguments passed to function except the expected one ("unused" arguments)
    * `ARGC` how many arguments were passed in
    * `ARGV0`, `ARGV1` ... the first, second, ... argument

## Macro
It's the same as function except that it doesn't have its own scope (inline in the caller side)
So we can change the global variables in macros but not functions
