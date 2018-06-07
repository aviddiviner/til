# Common Linux package names

I don't always remember package names for some of the core commands. This is useful when working in Docker containers and the like.

| Command   | `apt install`<sup>[1](#footnote1)</sup> | `apk add`<sup>[2](#footnote2)</sup> |
|-----------|---------------|------------|
| ip        | iproute2      | iproute2   |
| ping      | iputils-ping  | iputils    |
| dig       | dnsutils      | bind-tools |
| netstat   | net-tools     | net-tools  |
| ifconfig  | net-tools     | net-tools  |
| lsb_release | lsb-release | _(none)_   |
| setcap    | libcap2-bin   | libcap     |

Use `dpkg -S` to find out which package a command belongs to (on a host that already has it). For example:

```
$ dpkg -S `which ping`
iputils-ping: /bin/ping
```

And when in doubt, you can always search packages with `apt-cache search <name>`.

---

1. <a name="footnote1"></a>https://www.debian.org/distrib/packages#search_contents
2. <a name="footnote2"></a>https://pkgs.alpinelinux.org/contents?file=&path=&name=&branch=edge
