# KINIT and KLIST

```sh
[ec2-user@ip-172-31-6-157 hadoop-mapreduce]$ sudo su root
[root@ip-172-31-6-157 hadoop-mapreduce]# kadmin.local
Authenticating as principal weiner/admin@MITSARAVANAN.NYC with password.
kadmin.local:  getprincs
HTTP/ip-172-31-6-153.us-west-2.compute.internal@MITSARAVANAN.NYC
HTTP/ip-172-31-6-154.us-west-2.compute.internal@MITSARAVANAN.NYC
HTTP/ip-172-31-6-155.us-west-2.compute.internal@MITSARAVANAN.NYC
HTTP/ip-172-31-6-156.us-west-2.compute.internal@MITSARAVANAN.NYC
HTTP/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
K/M@MITSARAVANAN.NYC
christie@MITSARAVANAN.NYC
cloudera-scm@MITSARAVANAN.NYC
hdfs/ip-172-31-6-154.us-west-2.compute.internal@MITSARAVANAN.NYC
hdfs/ip-172-31-6-155.us-west-2.compute.internal@MITSARAVANAN.NYC
hdfs/ip-172-31-6-156.us-west-2.compute.internal@MITSARAVANAN.NYC
hdfs/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
hdfs@MITSARAVANAN.NYC
hive/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
hue/ip-172-31-6-153.us-west-2.compute.internal@MITSARAVANAN.NYC
kadmin/admin@MITSARAVANAN.NYC
kadmin/changepw@MITSARAVANAN.NYC
kadmin/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
kiprop/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
krbtgt/MITSARAVANAN.NYC@MITSARAVANAN.NYC
mapred/ip-172-31-6-153.us-west-2.compute.internal@MITSARAVANAN.NYC
oozie/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
weiner@MITSARAVANAN.NYC
yarn/ip-172-31-6-153.us-west-2.compute.internal@MITSARAVANAN.NYC
yarn/ip-172-31-6-154.us-west-2.compute.internal@MITSARAVANAN.NYC
yarn/ip-172-31-6-155.us-west-2.compute.internal@MITSARAVANAN.NYC
yarn/ip-172-31-6-156.us-west-2.compute.internal@MITSARAVANAN.NYC
yarn/ip-172-31-6-157.us-west-2.compute.internal@MITSARAVANAN.NYC
zookeeper/ip-172-31-6-153.us-west-2.compute.internal@MITSARAVANAN.NYC


```