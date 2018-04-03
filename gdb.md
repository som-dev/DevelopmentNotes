# gdb

## Attach
```
# attach to a pid
gdb attach 1234

# attach to a pid but find pid from running processes
gdb attach `ps -aef | grep [p]rocess-name | awk '{print $2}'`
```
## Launch
```
# launch an application with arguments
gdb --args /path/to/app --arg1 --arg2

# launch and attach to a core dump file
gdb /path/to/app core-dump-file
```
## Core and backtrace generation script
```
# save a series of commands like the following in a file and call gdb to attach to pid with --command=FILE
generate-core-file
thread apply all bt
detach
quit
```
## Useful Commands
```
# output of backtrace across all threads
thread apply all bt
# output of innermost 3 frames across all threads
thread apply all bt 3

# output of python backtrace across all threads (if you are debugging a python process)
thread apply all py-bt

# generate a core file
generate-core-file

# suppress displaying the static members of a class
set print static-members 0
# suppress displaying when threads start/exit
set print thread-events off
# no pause when outputting
set pagination off

# set where to look for shared libraries
show solib-search-path
set solib-search-path /path/to/app
# Use path as the system root. Any absolute shared library paths will be prefixed with path
set sysroot /path

# set a breakpoint on exit
break exit
```
