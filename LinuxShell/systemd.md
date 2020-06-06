# Systemd & Services
Linux中有三种管理service的方法:
1. systemd
2. service
3. init.d script (deprecated)

## Systemd
* `systemctl status [service_name]` 列出所有的services, 或者给定的service
* `systemctl stop <service_name>` 暂停service
* `systemctl start <service_name>` 启动service
* `systemctl restart <service_name>` 重启service, 会加载修改过的配置文件
* `systemctl reload <service_name>` 仅仅重新加载配置文件, 而不重启service, 会比`restart`稍微快一点
* `systemctl enable <service_name>` 建立service的链接, 使其开机会自动启动

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
