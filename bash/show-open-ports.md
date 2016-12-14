# Show open ports

Show all local ports that are listening for a connection.

## macOS

```bash
lsof -Pn -i4 | grep LISTEN
```

- `-P`: Show port numbers instead of port names.
- `-n`: Show network numbers instead of host names.
- `-i4`: Show IPv4 only.

```bash
netstat -ap tcp | grep LISTEN
```

- `-a`: Show the state of all sockets.
- `-p tcp`: Show TCP protocol statistics.

## Linux

```bash
netstat -ntlup
```

- `-n`: Show numerical addresses instead of symbolic host, port or user names.
- `-t`: Show TCP socket information.
- `-l`: Show only listening sockets. (Omitted by default.)
- `-u`: Show UDP socket information.
- `-p`: Show the PID and name of the program to which each socket belongs.
