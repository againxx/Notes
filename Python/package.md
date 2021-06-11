# Package

[Module](module.md) is a single python file

**Package** is a group of modules

## Define a Package
* a folder contains `__init__.py` is considered as a package
* package can have subpackages, just create a new folder and a new `__init__.py`
* When importing the package, Python searches through the directories on `sys.path` looking for the package directory and subdirectory

## Import a package
### Absolute Imports
* `import package_name` will execute all statement (including import statement) in the `__init__.py`
* `from package_name import subpackage / submodule` will import that subpackage or submodule into current namespace
* `from package_name import *` will only import names listed in `__all__` list
    - if `__all__` is not defined, it will execute all statement in the `__init__.py`,
      and import any submodules that were explicitly loaded by previous `import`

```python
import sound.effects.echo
import sound.effects.surround
from sound.effects import *
# Now, echo and surround can be used directly instead of using sound.effects.echo
```

### Relative Imports
* Relative imports will use leading dots. A single leading dot indicates a relative import, starting with the current package.
Two or more leading dots give a relative import to the parent(s) of the current package, one level per dot after the first.
* Relative imports must always use `from <> import`; `import <>` is always absolute

```python
from . import echo
from .. import formats
from ..filters import equalizer
```

## Miscellaneous
* `site-packages` third party libraries

## Reference
* [6. Modules — Python 3.9.2 documentation](https://docs.python.org/3/tutorial/modules.html#packages)
* [PEP 328 -- Imports: Multi-Line and Absolute/Relative | Python.org](https://www.python.org/dev/peps/pep-0328/)
