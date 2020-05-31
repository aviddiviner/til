# Dump packets with `tcpdump`

```
tcpdump -nnXSs 0 "port 53"
```

- `-nn`: don't look up hostnames in DNS and service names in /etc/services, for faster and cleaner output.
- `-X`: print each packet in hex and ASCII; useful for tracking headers and such.
- `-S`: print absolute rather than relative TCP sequence numbers.
- `-s 0`: by default tcpdump will only capture the beginning of each packet, using `0` here makes it capture complete packets.

Instead of `port 53` you can make more complicated rules like `src 10.0.2.4 and (dst port 3389 or 22)`.

Here is a good source: https://danielmiessler.com/study/tcpdump/
