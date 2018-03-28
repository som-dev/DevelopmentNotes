# Linux

## process searching
```
for p in `grep searchstr /path/to/config.xml | sort | cut -d'"' -f2` ; do if (ps -fU login | searchstr2 -v grep | grep -q $p) ; then echo "$p found"; else echo "$p not found" ; fi ; done

for p in `ps -aef | grep searchstr | grep -v grep | awk {'print $2'}` ; do kill $p ; done

for p in `ps -aef | grep searchstr | grep -v grep | awk {'print $2'}` ; do kill -9 $p ; done
```

## installs and package queries
```
yum list installed
apt list --installed
rpm -qa | grep pkgname
rpm -qi pkgname
```
