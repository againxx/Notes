# Telnet vs Netcat

## Telnet
* `telnet` specifically speaks the RFC 854 "Telnet" protocol
    - It recognizes certain bytes as Telnet options negotiation commands coming from the server, and will response to them appropriately
    - It will send its own at the beginning of each connection to the server (e.g. $TERM value and window size in lines*columns)
    - It will translate Unix LF line breaks to CR+LF version, and will recognize `Ctrl+]` as an escape key
* This makes `telnet` unsuitable for raw 8-bit TCP connections as it would mangle the transferred data
* However, it can still be used to interact with ASCII-based protocols such as FTP and SMTP
    - Many telnet clients do not initiate negotiation if connecting to a nonstandard port
* `telnet` is **TCP-only**

## Netcat
* `nc` is primarily an 8-bit clean TCP client. It will not alter any byte sent through it.
* It can be used with ASCII protocols just like telnet, but also can be used as a **pipe** into TCP for batch data transfer
* `nc` often offers non-TCP transports (UDP, sometimes SCTP, local Unix sockets)
* On the other hand, `nc` doesn't understand any protocols

## Summary
* If you are connecting to a Telnet server on port 23, use `telnet`
* If you need something like `cat` but for TCP, use `nc` or even `socat`
* If you need to send/receive non-text data, use `nc`/`socat` - avoid `telnet`
* If you want to manually type in SMTP or IRC or IMAP or HTTP commands, both tools will work fine.
    - `telnet` might work slightly better, as it converts line endings to CR+LF which some such servers also require

## Reference
[networking - What is the difference between telnet and netcat? - Super User](https://superuser.com/questions/1461609/what-is-the-difference-between-telnet-and-netcat)
