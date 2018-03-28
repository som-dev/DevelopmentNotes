# debugging

## strace
```
# 15 second strace of a running process
timeout -s SIGINT 15 "strace -p `ps -aef | grep [p]rocess-name | tr -s ' ' | cut -d' ' -f2` -ff -t o /tmp/out.txt"
```

## log cpu core usage every second
```
while true;
do
  logfile=monitor-log-`date +%Y-%m-%d`.txt
  mpstat -P ALL 1 1 | tail -n +5 | head `cat /proc/cpuinfo | grep processor | wc -l`
done
```
