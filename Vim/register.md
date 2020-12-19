# Register

* `:reg` 查看寄存器中的内容
* `put <reg>` put contents in <reg> into buffer for continuous editing
* `"<reg>y` yank back into <reg>
* Use `A-C` for append keys to `a-c`

## How to use registers
* In normal mode, use `"` to quote a certain register
* In insert mode, use `<Ctrl-r>` to insert the content of a register
* In command lien mode, use `@` to represent a register

## Builtin registers
* `%` current file path (relative or absolute)
* `#` alternate buffer register (switch using `<Ctrl-6>`)
* `_` black hole register (like `/dev/null`)
* `/` last search pattern register
* `=` expression register (useful in insert mode)
