# docker-debian

Base image for debian. 

### tags

* `10`: `debian:10-slim` with upgraded packages.
* `10-se`: `marcelofpfelix/debian:10` with [s6-overlay](https://github.com/just-containers/s6-overlay) v1 and [envtpl](https://github.com/mattrobenolt/envtpl).
* `10-dbg`: `marcelofpfelix/debian:10-se` with the debug packages installed.
* `11`: `debian:11-slim` with upgraded packages.
* `11-se`: `marcelofpfelix/debian:11` with [s6-overlay](https://github.com/just-containers/s6-overlay) v3 and [envtpl](https://github.com/mattrobenolt/envtpl).
* `11-dbg`: `marcelofpfelix/debian:11-se` with the debug packages installed.


Debug Packages:

```
ca-certificates
curl
dnsutils
inotify-tools
iproute2
iputils-ping
jq
mtr-tiny
netcat
openssl
procps
socat
traceroute
vim-tiny
wget
```

### Decisions

* There's no `rm -rf /var/lib/apt/lists/*`, to allow apt installs without a new update.
