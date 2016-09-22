# Installation prechecks

vm.swappiness
```sh
cat /proc/sys/vm/swappiness
30
sudo sysctl -w vm.swappiness=1
cat /proc/sys/vm/swappiness
1
```
noatime - File access time - disable this to improve hadoop performance. There was no non root volume to change this value
```sh
[ec2-user@ip-172-31-1-193 yarn-perf]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       50G  9.6G   41G  20% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
```
Reserve space
```sh
no non root volume to change this value
```
Ulimit
```sh
the maximum number of open file descriptors
[ec2-user@ip-172-31-1-193 yarn-perf]$ ulimit -n
1024
the maximum number of user processes
[ec2-user@ip-172-31-1-193 yarn-perf]$ ulimit -u
4096
```

Host Lookup 
 - sudo yum install bind-utils
```sh
[ec2-user@ip-172-31-1-193 ~]$ host 54.191.72.121
121.72.191.54.in-addr.arpa domain name pointer ec2-54-191-72-121.us-west-2.compute.amazonaws.com.
[ec2-user@ip-172-31-1-193 ~]$ host ec2-54-191-72-121.us-west-2.compute.amazonaws.com
ec2-54-191-72-121.us-west-2.compute.amazonaws.com has address 172.31.11.79
```
ntpd 
```sh
sudo yum install ntp
sudo chkconfig ntpd on
sudo service ntpd start
sudo service ntpd status
```
nscd 
```sh
sudo yum install ntp
sudo chkconfig ntpd on
sudo service ntpd start
sudo service ntpd status
```