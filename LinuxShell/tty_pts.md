# TTY vs PTS

> tty: TeleType writer, is a *native* terminal device, normally emulated by kernel this days
> pty: Pseudo Terminal, is a terminal device emulated by other program (xterm, tmux, ssh)
> pts: Pseudo Terminal Slave, is the slave part of the pty

## How pty works
* A pty is created by a process through `posix_openpt()` (which usually opens the special device `/dev/ptmx`),
  and is constituted by a pair of bidirectional character device.
  1. The master part, which is a file descriptor obtained by this process, is used to emulate terminal (receive and send characters to slave part)
  2. The slave part, which is anchored at filesystem as `/dev/pts/x` behaves like a native terminal device (`/dev/ttyx`).
     In most cases, a shell is started and uses it as a controlling terminal
## Commands
* `who` will show the logging users and their corresponding terminal device
* `tty` print the file name of the terminal connected to standard input

## Reference
* `man pts`
