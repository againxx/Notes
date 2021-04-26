# nm

* `-a` display all symbols including debugger only symbols
* `-A` precede each symbol by the name of file
* `-D` display dynamic symbols
* `-C` demangle low-level symbol name
* `-u` display only undefined symbol
* `-l` try to list filename and line number
* `-n` sort symbols numerically by their addresses

Output flags:
`Uppercase` for `global` symbols and `lowercase` for `local` symbol
* `T/t` symbol in text(code) section
* `D/d` initialized data section
* `B/b` bss data section that typically contains zero-initialized or uninitialized data
* `C/c` common symbol that is uninitialized data
* `U` undefined symbol
* `N` debuggin symbol
* `n` symbol in read-only section
* `R/r` symbol in read-only section?
