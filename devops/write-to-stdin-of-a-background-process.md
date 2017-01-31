# Write to STDIN of a background process

If you are using Linux, you can write to `/proc/(pid of the program)/fd/0`. The `fd` subdirectory contains the descriptors of all the opened files and file descriptor `0` is the standard input (`1` is stdout and `2` is stderr). For example:

    $ pidof myapp
    7417
    $ echo hello world > /proc/7417/fd/0

## Named pipe

If you know ahead of time that you want to write to STDIN, you could start the command with a named pipe (fifo) as its input:

    mkfifo /tmp/myfifo
    cat > /tmp/myfifo &
    echo $! > /tmp/catpid
    cat /tmp/myfifo | myapp &

The `cat > /tmp/myfifo &` prevents the command from receiving an EOF. At least one process must have the fifo open for writing or it will receive an EOF. The PID of this command is saved in `/tmp/catpid` for later killing.

If you've already started your command, you'll have to use a debugger such as `gdb` to attach to your process to redirect its `stdin` to the fifo:

    gdb -p PID
    call close(0)
    call open(0, "/tmp/myfifo", 0600)

And then `echo xyz > /tmp/myfifo` as you normally would. To send the EOF, just `kill $(cat /tmp/catpid)`. In the case of GDB, just quit GDB and an EOF will be sent.
