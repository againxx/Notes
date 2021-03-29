# PDB

[Summary of PDB Commands](https://realpython.com/lessons/python-debugging-pdb-summary/)

## Startup Debugger
Break into the debugger with just single line of Python code
```python
import pdb; pdb.set_trace()
# Python3.7 or later
breakpoint()
# You can automatically enable or disable all of the breakpoint() calls
# by modifying environment variables, how?

# Then launch the Python script regularly
```

pdb also supports **post-mortem debugging**, which will tell Python to drop you into a pdb prompt
as soon as an exception is reached
```shell
python3 -m pdb my_script.py
```

## Common Commands
| Commands    | Description                                            |
|-------------|--------------------------------------------------------|
| `l`         | list code (10 lines), next `l` will show next 10 lines |
| `l .`       | go back to show the first 10 lines                     |
| `ll`        | show local stack frame, usually the current function   |
| `p`         | evaluate expression                                    |
| `pp`        | pretty-print and will format the output of printing    |
| `n`         | stands for next, the equivalent of step over           |
| `s`         | stands for step, the equivalent of step into           |
| `c`         | continue execution up until the next breakpoint is hit |
| `a`         | show us the arguments passed into a function           |
| `<Enter>`   | repeat last command                                    |
| `h`         | see a list of available commands                       |
| `h <topic>` | show help for a command or topic                       |
| `h pdb`     | show the full pdb documentation                        |
| `q`         | quit out of the interactive debugger                   |

## Breakpoints
* Use the `b` command, followed by the module name and line number, to set breakpoint
* if we supply no module name, pdb will set breakpoint in the current module
* `b` with no line number will display a list of all current breakpoints
* `b <module>.<function>` will break when the function is entered
* `b <line>/<function>, <condition>` to set conditional breakpoints
```shell
b util:5
b 5
b

b util.get_path, not filename.startswith('/')
```

**Note:** when setting the breakpoint with a function name, the expression should use only function arguments or global variables,
that are available at the time the function is entered. Otherwise, the breakpoint will stop execution in function regardless
of the expression's value.

## Continuing Execution
* `unt` stands for `until` and will continue execution up until a specified line
* It behaves similarly to `n` command, when no line number is given
* The only difference: `unt` will iterate through entire loops automatically, instead of just moving forward one iteration
* `return` continue execution until current function's return statement

## Watches
* Use `display` to display variables or expression outputs each time it changes (add to watchlist)
* Running `display` without additional arguments will show us entire watchlist.
* `undisplay` will clear watchlist or remove the given variable from the watchlist
```shell
display char
display int
display
undisplay char
undisplay
```

## Stack Frames
* `w` stands for where, show stack trace, with the most recent frame at the bottom. An arrow indicates the current frame
* `u`  stands for up, move the current frame count (default one) levels up in the stack trace (to an older frame)
* `d`  stands for down, move the current frame count (default one) levels down in the stack trace (to a newer frame)

## PDB++
Open source drop-in replacement for `pdb` that adds support for colorful output, sticky mode and other conveniences.
* `sticky [start end]` command will keep a long list on the screen, above the interactive debugger.
    - every time the current position changes, the screen is repainted and the whole **function** shown
    - If start and end are given, only lines within that range will be displayed
* `longlist (ll)` command for listing current function, it seems original pdb also has this functionality
    - In case of post-mortem debugging, the line which actually raised the exception is marked with `>>`
* `interact` start an interactive interpreter containing all names defined in current scope
* `display <expression> / undisplay <expression>` evaluate expressions in display list every step, and print them every time their values changed
* prefer printing variable in scope first, use `!!<command_name>` to force the builtin command execution
* Use `@pdb.hideframe` to hide a function's associated stack frame from `where`, `up` and `down` commands.
