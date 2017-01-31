# `ifconfig` and `netstat` are deprecated

The **net-tools** package is deprecated. Use replacement tools from [**iproute2**](https://en.wikipedia.org/wiki/Iproute2).

| Legacy tool | Obsoleted by               | Notes                              |
|-------------|----------------------------|------------------------------------|
| arp         | ip neigh                   | Neighbors                          |
| ifconfig    | ip addr, ip link, ip -s    | Address and link configuration     |
| ipmaddr     | ip maddr                   | Multicast                          |
| iptunnel    | ip tunnel                  | Tunnels                            |
| route       | ip route                   | Routing tables                     |
| nameif      | ifrename, ip link set name | Rename network interfaces          |
| netstat     | ip -s, ss, ip route        | Show various networking statistics |
| mii-tool    | [ethtool](https://en.wikipedia.org/wiki/Ethtool) | NIC parameters |

Another handy substitute for `netstat -ntlup` is `lsof -Pn -i | grep LISTEN`.
