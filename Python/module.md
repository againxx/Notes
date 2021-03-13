# Module

## Basic concepts
* A module can contain executable statements as well as function definitions
    - statements are executed only the *first* time the module name is encountered in an import statement
    - for dynamic reload module, use `import importlib; importlib.reload(module_name)`
* Each module has its own private symbol table, which is used as a global symbol table by all functions defined within it
* `from module_name import *` this imports all names except those begin with `_`

## Module Special Variable
* `__name__` module's name
