# Teragen# command
```sh
time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Ddfs.block.size=67108864 5120000000 /user/christie/tgen64
```
Output of the time command

```sh
real    14m26.029s
user    0m8.290s
sys     0m0.499s
```
The command and output of hdfs dfs -ls /user/christie/tgen64

```sh
[root@ip-172-31-6-157 krb5kdc]# hdfs dfs -ls /user/christie/tgen64
Found 1 items
drwxr-xr-x   - christie christie          0 2016-09-23 15:00 /user/christie/tgen64/_temporary
```