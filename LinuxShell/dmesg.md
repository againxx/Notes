# Dmesg

Review and monitor hardware device and driver messages from the kernel's own *ring buffer*

## Ring buffer
In Linux, _booting_ and _startup_ are two distinct phases
* The boot processes ( **UEFI** and **Grub** ) take the initialization of the system to the point where
    - The kernel is loaded into memory
    - The kernel is connected to the initial ramdisk ( **initrd** or **initramfs** )
    - **systemd** is started
* The startup processes then continue to complete the initialization of the system
    - In the very early stages, logging daemons such as syslogd or rsyslogd are **not** yet running
    - To avoid losing notable error messages and warnings, the kernel contains a **ring buffer** for message storing

* A ring buffer is just a fixed size memory. And when it is full, newer messages overwrite the oldest (circular buffer)
* It is mainly used to store information such as
    - initialization of device drivers
    - messages from hardware
    - messages from kernel modules

## Dmesg command
* `sudo dmesg | bat`
* `sudo sysctl -w kernel.dmesg_restrict=0` to remove the need for sudo
* `dmesg -L` forcing color output
* `dmesg -H` by default it use a timestamp notation of seconds and nanoseconds since the kernel started, use `-H` for human friendly format
* `dmesg -T` human readable timestamp (timestamps are rendered as standard dates and times)
* `dmesg --flow` wait for messages arriving, things that will generate messages includes
    - a change in hardware connection
    - update or add a kernel module
* `dmesg -l <level1>,<level2>` to see only specified log level
    - **emerg**: system is unusable
    - **alert**: action must be taken immediately
    - **crit**: critical conditions
    - **err**: error conditions
    - **warn**: warning conditions
    - **notice**: normal but significant condition
    - **info**: informational
    - **debug**: debug-level messages
* `dmesg -f <facility1>,<facility2>` messages can also be grouped into categories called _facilities_
    - **kern**: kernel messages
    - **user**: user-level messages
    - **mail**: mail system
    - **daemon**: system daemons
    - **auth**: security / authorization messages
    - **syslog**: internal syslogd messages
    - **lpr**: line printer subsystem
    - **news**: network news subsystem
* `dmesg -x` show the facility and level as human-readable prefix to each line

## Available information
* Linux kernel command line

## Typical usage flow
1. Review mesages from the highest _level_ down through lower level, looking for any errors or warnings that mention the hardware item,
or may have a bearing on the issue.
2. Search for any mention of the appropriate _facility_ to see whether they contain any useful information
3. Pipe dmesg through grep and look for related _strings_ or _identifiers_ such as product manufacturer or model numbers
4. Pipe dmesg through grep and look for generic terms like "gpu" or "storage", or terms such as "failure", "failed" or "unable"
5. Use the `--follow` option and watch dmesg messages in real-time

## Reference
[How to Use the dmesg Command on Linux](https://www.howtogeek.com/449335/how-to-use-the-dmesg-command-on-linux/)
