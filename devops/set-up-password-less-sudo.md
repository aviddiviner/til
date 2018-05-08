# Set up password-less `sudo`

For example, to have `haproxy` run as `sudo` without requiring a password (on Mac):

```bash
sudo mkdir -pv /etc/sudoers.d
echo '%admin ALL=(ALL) NOPASSWD: /usr/local/bin/haproxy *' \
  | sudo tee /etc/sudoers.d/haproxy
```

The path (in this case `/usr/local/bin/haproxy`) is the full path to the binary. It can then be invoked normally with `sudo haproxy ...`