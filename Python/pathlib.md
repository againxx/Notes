# Pathlib

Offers classes representing filesystem paths with semantics appropriate for different operating systems. (new in 3.4)

## Basic Use
```python
from pathlib import Path
p = Path('.')
[x for x in p.iterdir()] # iterates the dir

q = p / 'foo' / 'bar' # join paths
q = p.joinpath('foo').joinpath('bar') # another way to join paths

q.resolve() # get absolute path
str(q) # cast Path into a string

# List python source files in this directory tree
list(p.glob("**/*.py"))
```

## Useful Methods

| Name                | Usage                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------------|
| `home()`            | return a path object representing the home dir                                                             |
| `cwd()`             | return a path object representing current working directory in shell                                       |
| `exists()`          | whether points to an existing file or directory                                                            |
| `is_dir()`          | return `True` if points to a directory                                                                     |
| `is_file()`         | return `True` if points to a regular file (or a symbolic link points to)                                   |
| `is_symlink()`      | return `True` if points to a symbolic link                                                                 |
| `rmdir()`           | remove this dir, the dir must be empty                                                                     |
| `mkdir()`           | create a new directory                                                                                     |
| `chmod(0o755)`      | change the file mode and permissions                                                                       |
| `rename(target)`    | rename this file or directory to the given target, return a new path instance                              |
| `glob(pattern)`     | glob the given relative pattern in the directory, `**` pattern means this directory and all subdirectories |
| `read_text()`       | read the whole file in text mode, close it after reading                                                   |
| `read_bytes()`      | read the whole file in binary mode, close it                                                               |
| `write_text(data)`  | write data in text mode, close it                                                                          |
| `write_bytes(data)` | write data in binar mode, close it                                                                         |

## Useful Properties

| Name      | Value                                                         |
|-----------|---------------------------------------------------------------|
| `parent`  | the logical ancestor `/a/b/c/d` -> `/a/b/c`                   |
| `parents` | an immutable sequence of the logical ancestors                |
| `parts`   | a tuple: '/usr/bin/python3' -> ('/', 'usr', 'bin', 'python3') |
| `name`    | a string representing the final path component                |
| `suffix`  | the file extension of the final component, if any             |
| `stem`    | the final path component, without its suffix                  |
