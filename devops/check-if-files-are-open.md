# Check if files are open

To check if files are currently opened by a process:

```
find /path/to/folder -exec fuser -v {} +
```
