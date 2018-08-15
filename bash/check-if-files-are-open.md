# Check if files are open

Check if files in a folder are open by any process:

```bash
find /path/to/folder -exec fuser -v {} +
```
