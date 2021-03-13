# Package

[Module](module.md) a single python file

**Package** a group of modules

## Different Ways to Find Module
* `sys.path` includes a list of path to search for modules
* set environment variable `PYTHONPATH`

## Define a Package
* a folder contains `__init__.py` is considered as a package
* package can have subpackages, just create a new folder and a new `__init__.py`

## Import a package
* `import package_name` will execute all statement (including import statement) in the `__init__.py`
* `from package_name import subpackage / submodule` will import that subpackage or submodule into current namespace
* `from package_name import *` will only import names listed in `__all__` list

## Miscellaneous
* `site-packages` third party libraries

## Reference
[6. Modules — Python 3.9.2 documentation](https://docs.python.org/3/tutorial/modules.html#packages)
