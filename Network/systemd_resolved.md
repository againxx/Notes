# Systemd-Resolved

* Systemd-resolved runs as a daemon. All programs wanting to translate domain names to network addresses will talk to it.
* This replaces previous lookup mechanism where each program individually talks to remote servers and there is no **shared cache**.
* Systemd-resolved is a "stub resolver" - it doesn't resolve all names itself, but forwards the queries to a remote server.

## Advantages
1. The daemon caches answers, which speeds answers for frequently used names.
2. The daemon remembers which servers are non-responsive
3. Individual programs only talk to the daemon over a local transport and are more isolated from the network
4. The daemon supports fancy rules which specify which name servers should be used for which domain names

## Split DNS
Systemd-resolved first picks one or more interfaces which are appropriate for a given name, and then queries one of the name servers attached to that interface.
This is known as "split DNS".

There are two flavors of domains attached to a network interface. They both specify that the given domain and any subdomains are appropriate for that interface.
* _routing domains_
    - prefixed with the tilde `~` character
* _search domains_, have additional function that single-label names are **suffixed** with that search domain before being resolved.
    - For example, a lookup for `www` is treated as `www.ustc.edu.cn` if the search domain is `ustc.edu.cn`

* If you have multiple interfaces with search domains, single-label names are suffixed with all search domains and resolved in parallel
* For multi-label names, no suffixing is done. The longest match wins. When there are multiple matches of the same length on different interfaces, they are resolved in parallel
* When an interface has a routing domain `~.`, it always matches any names, but with the shortest possible length.
* Finally, if no routing or search domains matched, the name is routed to all interfaces that have at least one name server attached.

## Lookup routing
Here routing means the process of deciding which servers to ask for a given domain name, **rather than** the process of deciding where to send network packets

```shell
$ resolvectl domain

Global:
Link 4 (wlp4s0): ~.
Link 18 (hub0): 
Link 26 (tun0): redhat.com

$ resolvectl dns

Global:
Link 4 (wlp4s0): 192.168.1.1 8.8.4.4 8.8.8.8
Link 18 (hub0):
Link 26 (tun0): 10.45.248.15 10.38.5.26
```

## Configuration
* Configuration files at
    - `/etc/systemd/resolved.conf`
    - `/etc/systemd/resolved.conf.d/*.conf`
    - `/run/systemd/resolved.conf.d/*.conf`
    - `/usr/lib/systemd/resolved.conf.d/*.conf`

* Alternatively, `resolvectl` can be used for configuration (it's just a wrapper around the D-Bus API)
* Finally, `resolvconf` provides similar functionality in a form of compatibility

D-Bus API allows other programs to dynamically change the configuration, such as NetworkManager or systemd-networkd
* Normally, NetworkManager will tell systemd-resolved to use the name servers and search domains received in a DHCP lease on some interface

## Reference
* [systemd-resolved: introduction to split DNS - Fedora Magazine](https://fedoramagazine.org/systemd-resolved-introduction-to-split-dns/)
* [Understanding systemd-resolved, Split DNS, and VPN Configuration – Michael Catanzaro's Blog](https://blogs.gnome.org/mcatanzaro/2020/12/17/understanding-systemd-resolved-split-dns-and-vpn-configuration/)
