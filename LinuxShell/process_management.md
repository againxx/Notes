# Process Management

## Fork / Exec
* When bash execute a external command, it first **forks** itself and uses **exec** to replace current executable image
* We can also use `exec` directly in the bash to replace current process

## Ps command

### common options
| Option      | Description                         |
|-------------|-------------------------------------|
| -e          | select all processes                |
| -o          | control output format               |
| -u          | select by effective user ID or name |
| -U          | select by real user ID or name      |
| --sort      | sort the selected processes         |
| -- pid / -p | select by PID                       |
| --ppid      | select by PPID                      |

**EUID vs RUID**:
* RUID: real user ID identifies the user who created the process
* EUID: effective user ID describes whose file access permissions are used by the process

### process state
| Code | Description                                                |
|------|------------------------------------------------------------|
| I    | Idle kernel thread                                         |
| R    | running or runnalbe                                        |
| S    | interruptible sleep (waiting for an event)                 |
| D    | uninterruptible sleep (waiting for I/O such as disk drive) |
| T    | stopped by job control signal                              |
| t    | stopped by debugger during the tracing                     |
| Z    | zombie process, terminated but not reaped by its parent    |

For BSD formats only
| Code | Description                        |
| <    | high-priority (not nice)           |
| N    | low-priority (nice)                |
| s    | is a session leader                |
| l    | is multi-threaded                  |
| +    | is in the foreground process group |

**Niceness**: a property that grant more importance to a process i.e. more execution time. A process with high priority is said to be less *nice*, because it's taking more of the CPU time

### headers

| Name | Description                                                     |
|------|-----------------------------------------------------------------|
| VSZ  | virtual memory size in KiB                                      |
| RSS  | resident set size, non-swapped physical memory size in KiB      |
| PRI  | priority, higher number means lower priority                    |
| NI   | nice value, ranges from 19 (nicest) to -20 (not nice to others) |

## Foreground / Backgroud
* We can start process directly into background with a trailing `&`
* All we can suspend it by `Ctrl-z` and restart it use `bg`

## Relationship with signals
* `Ctrl-c`: SIGINT (2)
* `Ctrl-z`: SIGTSTP (20)
* `Ctrl-\`: SIGQUIT (3)
* `fg/bg`: SIGCONT (18)

## Process Group
* A process group are a collection of related processes sharing the same PGID (Process Group ID)
* A common **misconception** is that killing the parent process will kill the children processes too
* Each process group has a group leader whose process id is the same as the PGID of all the processes inside the group
* We can use `kill -- -PGID / kill -SIGxxx -PGID` to kill a process group
