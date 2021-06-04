# Special Parameters in Bash

* `$*` all positional parameters ($1, $2, ...)
    - when `$*` in quote, bash will use first character in `IFS` for delimiter
    - when unquoted, always use space for delimiter
* `$@` same as above, but always use space for delimiter
* `$#` number of positional parameters
* `$?` exit code for last command
* `$$` current script shell PID (don't change in subshell)
* `$!` PID of the most recent job placed in background
* `$_` last parameter of the previous command
