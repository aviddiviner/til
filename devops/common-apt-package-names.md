# Common `apt` package names

I don't always remember package names for some of the core commands. This is useful when working in Docker containers and the like.

| Command   | `apt install` |
|-----------|---------------|
| ip        | iproute2      |
| ping      | iputils-ping  |
| dig       | dnsutils      |
| netstat   | net-tools     |
| ifconfig  | net-tools     |
| lsb_release | lsb-release |

Use `dpkg -S` to find out which package a command belongs to (on a host that already has it). For example:

```
$ dpkg -S `which ping`
iputils-ping: /bin/ping
```

And when in doubt, you can always search packages with `apt-cache search <name>`.
