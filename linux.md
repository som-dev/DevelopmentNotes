# Linux

## redirects
```
app > stdout.txt
app >> append-stdout.txt
app 2> stderr.txt
app > stdout.txt 2>stderr.txt
app 2>&1 > stdoutanderr.txt
```

## process searching
```
# find processes in a config file
for p in `grep searchstr /path/to/config.xml | sort | cut -d'"' -f2` ; do if (ps -fU login | searchstr2 -v grep | grep -q $p) ; then echo "$p found"; else echo "$p not found" ; fi ; done

# graceful kill of processes matching a searchstr
for p in `ps -aef | grep searchstr | grep -v grep | awk {'print $2'}` ; do kill $p ; done

# abrupt kill of processes matching a searchstr
for p in `ps -aef | grep searchstr | grep -v grep | awk {'print $2'}` ; do kill -9 $p ; done
```

## installs and package queries
```
yum list installed
apt list --installed
rpm -qa | grep pkgname
rpm -qi pkgname
```

# sql command-line tools
```
sqlcmd -Q"query command" -S severname -U login -P password -l 30
bcp  'table' in 'filename' -n -S servername -U login -P password
```
