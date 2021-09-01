# Process Management

## Fork / Exec
* When bash execute a external command, it first **forks** itself and uses **exec** to replace current executable image
* We can also use `exec` directly in the bash to replace current process

## Ps command

### common options
| Option      | Description          |
|-------------|----------------------|
| -e          | select all processes |
| -- pid / -p | select by PID        |
| --ppid      | select by PPID       |

### process state
| Code | Description                                             |
|------|---------------------------------------------------------|
| I    | Idle kernel thread                                      |
| R    | running or runnalbe                                     |
| S    | interruptible sleep                                     |
| T    | stopped by job control signal                           |
| t    | stopped by debugger during the tracing                  |
| Z    | zombie process, terminated but not reaped by its parent |

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
