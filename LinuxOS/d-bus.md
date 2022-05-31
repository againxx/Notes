# D-Bus

D-Bus is a message bus system (software bus) for inter-process communication, it has a three layer architecture:
1. D-Bus **protocol** for communication between two processes
2. low-level C library which implements D-Bus protocol **libdbus**
3. D-Bus daemon, like systemd can have multiple instances at the same time
    - system-wide message bus
        - used for broadcasting system events like adding or removing devices, etc
    - each user session
        - used for some desktop applications

![D-Bus Demonstration](http://images.againxx.cn/interprocess-communication-using-dbus.png =750x)
