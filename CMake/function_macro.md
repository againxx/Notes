# Function & Macro

```cmake
function(print var)
    message("${var} = ${${var}}")
endfunction()
```

* `ARGN` all arguments passed to function
* `ARGC` how many arguments were passed in
* `ARGV0`, `ARGV1` ... the first, second, ... argument
