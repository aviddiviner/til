# Trim lines off a large file

Shave the last line (N lines) off a file:

```bash
truncate -s -$(tail -n1 file | wc -c) file
```
