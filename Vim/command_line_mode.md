# Command Line Mode

* use `q:` in normal mode to open the editable buffer for all history commands(command-line window)
* `<C-f>` in command line mode has the same effect as `q:`, useful in `<C-r>=`
* in command-line window
    - use `<Enter>` to execute the command
    - use `<C-c>`(I remap it to `<C-c><C-x>`) to continue in command line mode
    - use `:q` to discard the command line and go back to normal mode
* `<C-b>` go to the beginning of the command
* `<C-e>` go to the end of the command
* `:read` 可以将命令的输出写入buffer
