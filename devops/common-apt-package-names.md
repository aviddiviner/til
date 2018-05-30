# Common `apt` package names

I don't always remember package names for some of the core commands. This is useful when working in Docker containers and the like.

| Command  | `apt install` |
|----------|---------------|
| ip       | iproute2      |
| ping     | iputils-ping  |
| dig      | dnsutils      |
| netstat  | net-tools     |
| ifconfig | net-tools     |

And when in doubt, you can always search with `apt-cache search <name>`.
