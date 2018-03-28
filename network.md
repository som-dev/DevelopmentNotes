# Network

## Multicast related troubleshooting
```
cat /proc/sys/net/ipv4/conf/enp0s3/rp_filter
sudo sysctl -w net.ipv4.conf.enp0s3.rp_filter=0

sudo ip route add 224.0.0.0/4 dev enp0s3
sudo route del -net 244.0.0.0/4
```

## iptables
```
# add rule to drop from a specific address
sudo iptables -I INPUT -d 1.2.3.4 -j DROP
# list rules
sudo iptables -L INPUT
# delete above rule
sudo iptables -D INPUT -d 1.2.3.4 -j DROP
```

# stats
```
cat /proc/net/udp
ip -s addr
netstat -suna
```

# helper script for OS-level dropped counts
```
# output dropped msg stats every so often
# note that the position of stats differ across distros
while true;
do
  logfile=monitor-log-`date +%Y-%m-%d`.txt
  timestamp=$(date +'%Y-%m-%d %R:%S')
  #echo "$timetamp enp0s3: " `ifconfig | grep enp0s3 -A 3 | grep dropped` >> $logfile
  echo "$timetamp enp0s3: " `ip -s addr show enp0s3 | grep RX -A 1 | tail -1 | awk '{print $4}'` >> $logfile
  echo "$timetamp UDP: " `netstat -suna | grep 'packet receive errors'` >> $logfile
  echo "$timetamp UDP: " `netstat -suna | grep 'receive buffer errors'` >> $logfile
  sleep 3600
done

# find the difference in stats between the beginning and the end of a file
# note that the position of stats differ across distros
if [ -z "$1" ]
then
  echo "filename not supplied"
  exit
fi
file=$1

nic_str="enp0s3"
udp_pkt_rcv_str="packet receive errors"
udp_rcv_buf_str="receive buffer errors"

nic_drop_begin=$(head -50 $file | grep "$nic_str" | head -1 | awk '{print $2}')
udp_pkt_rcv_err_begin=$(head -50 $file | grep "$udp_pkt_rcv_str" | awk '{print $2}')
udp_rcv_buf_err_begin=$(head -50 $file | grep "$udp_rcv_buf_str" | awk '{print $2}')
nic_drop_end=$(tail -50 $file | grep "$nic_str" | tail -1 | awk '{print $2}')
udp_pkt_rcv_err_end=$(tail -50 $file | grep "$udp_pkt_rcv_str" | tail -1 | awk '{print $2}')
udp_rcv_buf_err_end=$(tail -50 $file | grep "$udp_rcv_buf_str" | tail -1 | awk '{print $2}')
let nic_drop=$nic_drop_end-$nic_drop_begin
let udp_pkt_rcv_err=$udp_pkt_rcv_err_end-$udp_pkt_rcv_err_begin
let udp_rcv_buf_err=$udp_rcv_buf_err_end-$udp_rcv_buf_err_begin
echo "nic drops:                 $nic_drop"
echo "udp packet receive errors: $udp_pkt_rcv_err"
echo "udp receive buffer errors: $udp_rcv_buf_err"

```
