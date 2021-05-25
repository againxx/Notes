# Systemd & Services
Linux中有三种管理service的方法:
1. systemd
2. service
3. init.d script (deprecated)

## Systemd
systemd 的unit包括但不仅限于service, 所以适用面要更广一些

### systemctl
* `systemctl status [unit_name]` 列出所有的unit, 或者给定的unit
* `systemctl [list-units]` list running units
* `systemctl --failed` list failed units
* `systemctl stop <unit_name>` 暂停unit
* `systemctl start <unit_name>` 启动unit
* `systemctl restart <unit_name>` 重启unit, 会加载修改过的配置文件
* `systemctl reload <unit_name>` 仅仅重新加载配置文件, 而不重启unit, 会比`restart`稍微快一点
* `systemctl enable <unit_name>` 建立unit的链接, 使其开机会自动启动
* `systemctl enable --now <unit_name>` 建立unit的链接, 使其开机会自动启动, 并马上start该unit
* `systemctl disable <unit_name>`
* `systemctl disable --now <unit_name>`
* `systemctl daemon-reload` 重新扫描指定目录中的unit文件, 建立依赖树, 注意不同于`reload`

### systemd timer
* `systemd-analyze calendar <calendar_event_specification>` 分析指定的calendar时间, 以及下次什么时候发生

### journalctl

### user instance
systemd offers the users the ability to manage services under the user's control with a *per-user instance*

User's units are located in following directories (ordered by **ascending** precedence)
1. `/usr/lib/systemd/user/` units provided by installed packages
2. `~/.local/share/systemd/user/` units of packages that have been installed in the home directory
3. `/etc/systemd/user/` system-wide user units placed by the system administrator
4. `~/.config/systemd/user/` where user puts their own units

When a systemd user instance starts, it brings up the per-user target `default.target` like `multi-user.target` for system instance


## Service
* `service --status-all` 类似`systemctl status`
* `service <service_name> status` 列出某个具体的service的状态
* `service <service_name> stop` 暂停service
* `service <service_name> start`
* `service <service_name> restart`

## Init.d Script
* `/etc/init.d/<service_name> status`
* `/etc/init.d/<service_name> stop`
* `/etc/init.d/<service_name> start`
* `/etc/init.d/<service_name> restart`

## Reference
[Use systemd timers instead of cronjobs | Opensource.com](https://opensource.com/article/20/7/systemd-timers)
