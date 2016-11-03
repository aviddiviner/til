# Step-by-step debugging on the console

Just add the following lines to your script at the point you'd like to start the debugger:

```python
import pdb
pdb.set_trace()
```

There are a few commands you can then issue, which are documented on the [pdb](http://docs.python.org/library/pdb.html) page.

Some useful ones to remember are:

- `b`: set a breakpoint
- `c`: continue debugging until you hit a breakpoint
- `s`: step through the code _(step in)_
- `n`: to go to next line of code _(step over)_
- `l`: list source code for the current file (default: 11 lines including the line being executed)
- `u`: navigate up a stack frame
- `d`: navigate down a stack frame
- `p`: to print the value of an expression in the current context
