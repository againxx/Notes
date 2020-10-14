# Core Dump

Core dump is a file that records the process's memory when the program crashes, it's an important aid for debugging.

* Use `ulimit -c` to show current core dump size limit (default is 0, so no core dump will be generated)
* Use `ulimit -c unlimited` to set core dump size limit to be infinite
* Then when the program crashed, a file named `core` will occur in the current directory
* We can now use `gdb <program_name> core` to load the core dump into the debugger, and check the last status of the program
* Be careful, core dump file may be very large and take lots of space
