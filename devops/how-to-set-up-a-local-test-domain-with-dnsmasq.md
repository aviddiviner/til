# How to set up a local test domain with `dnsmasq`

## Use the `.test` TLD

[RFC-2606](http://tools.ietf.org/html/rfc2606) reserves 4 different TLDs for testing and documentation examples:

* `.test`
* `.example`
* `.invalid`
* `.localhost`

It also reserves these second-level addresses:

* `example.com`
* `example.net`
* `example.org`

## Set up `dnsmasq` and resolvers

1. Install [Homebrew](https://brew.sh/) and [Homebrew Services](https://github.com/Homebrew/homebrew-services) if you haven't already.

2. `brew install dnsmasq`, edit its config (`/usr/local/etc/dnsmasq.conf`, assuming your `brew --prefix` is `/usr/local`) and enable only these options:

    ```
    no-resolv
    address=/.localdomain/127.0.0.1
    address=/.test/127.0.0.1
    ```

3. Create `/etc/resolver` directory, and add 127.0.0.1 (*dnsmasq*) as nameserver for our TLDs:

    ```
    % sudo mkdir -pv /etc/resolver
    % sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/localdomain'
    % sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/test'
    ```

4. System Preferences > Network > Wi-Fi > Advanced… > Search Domains > add `localdomain` to the list.

5. Start / restart *dnsmasq* and check that it is listening. Ping to test.

    ```
    % sudo brew services restart dnsmasq
    % lsof -Pn -i | grep LISTEN
    % ping foo
    PING foo.localdomain (127.0.0.1): 56 data bytes
    64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.033 ms
    ^C
    % ping foo.test
    PING foo.test (127.0.0.1): 56 data bytes
    64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.044 ms
    ^C
    % dig @127.0.0.1 foo.test
    ```

## References

* https://iyware.com/dont-use-dev-for-development/
* https://superuser.com/questions/184361/what-is-the-search-domains-field-for-in-the-tcp-ip-dns-settings-control-panel
* https://medium.com/@narakuw/brew-install-dnsmasq-in-macos-sierra-26021c824be8
* https://serverfault.com/questions/799200/bind-dnsmasq-dns-to-just-localhost-127-0-0-1
