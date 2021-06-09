# apt & apt-get
0. `apt`整合了`apt-get`和`apt-cache`中的精华
1. `sudo apt update`
    * Hit(命中): 尝试了，发现没有新版本
    * Ign(忽略): 太新了，没必要尝试；或者出现错误，但是不要紧
    * Get(获取): 存在新版本
2. `sudo apt upgrade`和`sudo apt full-upgrade`: 后者可能会删除已经安装的包
3. `sudo apt install -y` 默认yes
4. `sudo apt install --no-upgrade` 如果存在则不更新
5. `sudo apt install --only-upgrade` 如果不存在则不安装
6. `sudo apt install <package_name>=<version_number>`
7. `sudo apt remove`和`sudo apt purge`: purge同时删除配置文件，能对已经remove的包purge
8. `apt search <search_term>`
9. `apt show <package_name>` can show package dependencies
10. `apt list --upgradeable`
11. `apt list --installed`
12. `apt list --all-versions`列出适合当前系统的所有包
13. `sudo apt autoremove` 删除为了满足依赖而自动安装的包
14. `sudo apt edit-sources` 编辑sources.list文件
15. `apt policy` 可以列出所有的源，包括PPA
16. `sudo add-apt-repository ppa:<ppa_repository_name>/<ppa>`添加PPA，`sudo add-apt-repository --remove ppa:<ppa_repository_name>/<ppa>`删除PPA
17. 也可通过删除`/etc/apt/sources.list.d`下的文件来删除PPA
18. `sudo apt-mark hold <package_name>` 来锁定包，不让其自动更新
19. `apt-mark showhold` 列出当前锁定的包
20. `sudo apt-mark unhold <package_name>` 解除锁定
21. `sudo apt -o Acquire::socks::proxy="socks5://127.0.0.1:1080/" update` 临时使用socks5代理

## Other apt-related tools
* `apt-file show/list <package_name>` list contents of a package
* `apt-file search <relative_path>/<file_name>` search which package contains the given file
* `apt-cache search` 类似`apt search`
