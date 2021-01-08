# Source & Dot

* both `.` and `source` are used to read and execute commands from the _filename_ argument in the current shell context.
* `source` is a synonym for dot/period `.` in bash, but not in POSIX sh, so for maximum compatibility use the period.
* if the script is run just as _filename_ (with shebang), then a separate subshell (with a completely separate set of variables) would be spawned to run the script.
* `source` is a bash built-in command and cannot be use with `find -exec`?
