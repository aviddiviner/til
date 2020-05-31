# Keep two folders in sync across hosts

Using [inotifywait](https://linux.die.net/man/1/inotifywait) to wait for filesystem changes and [rsync](https://linux.die.net/man/1/rsync) to copy the changes across hosts.

```bash
while inotifywait -r /directory/*; do
    rsync -avz /directory /target
done
```
