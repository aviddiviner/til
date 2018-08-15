# Trim lines off a large file

Shave the last N lines off a file:

```bash
truncate -s -$(tail -n1 file | wc -c) file
```
