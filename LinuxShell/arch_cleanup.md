# Archlinux Cleanup

## 1. Clean package cache
* `/var/cache/pacman/pkg/`
    - pacman will not remove the old or uninstalled packages automatically
    - `sudo pacman -Sc` remove cached packages that are not currently installed
    - `sudo pacman -Scc` remove all packages
    - `paccache` delete all cached version except for the most recent 3 versions
* `~/.cache/yay/`
    - `yay -Sc`

## 2. Remove unused packages (orphans)
* `sudo pacman -Qtdq`
* `sudo pacman -Rsn $(pacman -Qtdq)`

## 3. /home cache files
* `bleachbit`

## 4. Remove duplicates, empty files, empty directories and broken symlinks
* `rmlint`

## 5. Clean systemd journal
* systemd stores its logs at `/var/log/journal`, taking up 10% of your system size by default
* only keep 50MB the latest logs, `sudo journalctl --vacuum-size=50M`
* or by time limit, last 4 weeks, `sudo journalctl --vacuum-time=4weeks`
* edit `SystemMaxUse` in `/etc/systemd/journald.conf`

## Reference
[How to clean Arch Linux | Average Linux User](https://averagelinuxuser.com/clean-arch-linux/)
