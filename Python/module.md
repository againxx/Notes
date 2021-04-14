# Module

## Basic concepts
* A module can contain executable statements as well as function definitions
    - statements are executed only the *first* time the module name is encountered in an import statement
    - for dynamic reload module, use `import importlib; importlib.reload(module_name)`
* Each module has its own private symbol table, which is used as a global symbol table by all functions defined within it
* `from module_name import *` this imports all names except those begin with `_`

## Module Special Variable
* `__name__` module's name
    - when the module is executed as script, the `__name__` will be set to `"__main__"`

## Where to Find Modules
* Firstly, built-in modules
* Secondly, searches in `sys.path`, which includes a list of path to search for modules / packages and is initialized by
    - the directory containing current script (or current directory when no script is specified)
    - environment variable `PYTHONPATH`
    - the installation-dependent default
* Finally, we can modify `sys.path` to include other modules

## "Compiled" Python Files
* Python caches the compiled version of each module in `__pycache__` directory under the name `module.version.pyc`
* the module `compileall` can create .pyc files for all modules in a directory

## dir() Function
* The built-in `dir(module_name)` function is used to determine which names the module defines
* Without arguments, it lists the all types of names defined by you currently (variables, functions, modules)
* Use `import builtins; dir(builtins)` to list builtin names
