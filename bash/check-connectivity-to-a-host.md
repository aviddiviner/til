# Check connectivity to a host

Normally, to check if you can connect to a given host/port, you'd use something like `telnet`.

```
% telnet 192.168.25.111 5672
Trying 192.168.25.111...
Connected to 192.168.25.111.
Escape character is '^]'.
^CConnection closed by foreign host.
```

Instead, use `netcat`. You get more verbose output, with less `^C`.

```
% nc -zv 192.168.25.111 5672
found 0 associations
found 1 connections:
     1: flags=82<CONNECTED,PREFERRED>
        outif tap0
        src 192.168.25.200 port 51043
        dst 192.168.25.111 port 5672
        rank info not available
        TCP aux info available

Connection to 192.168.25.111 port 5672 [tcp/amqp] succeeded!
```

```
% nc -zv 192.168.25.111 9999
nc: connectx to 192.168.25.111 port 9999 (tcp) failed: Connection refused
```
