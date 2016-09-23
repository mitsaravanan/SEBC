mysql> SHOW GRANTS for 'rman'@'ip-172-31-6-157.us-west-2.compute.internal';
+----------------------------------------------------------------------------------------------------------------------------------------------+
| Grants for rman@ip-172-31-6-157.us-west-2.compute.internal                                                                                   |
+----------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'rman'@'ip-172-31-6-157.us-west-2.compute.internal' IDENTIFIED BY PASSWORD '*819397F8B454D58DA4E9F42A88A4873756B8C96D' |
| GRANT ALL PRIVILEGES ON `rman`.* TO 'rman'@'ip-172-31-6-157.us-west-2.compute.internal'                                                      |
+----------------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)


mysql> SHOW GRANTS for 'hive'@'ip-172-31-6-157.us-west-2.compute.internal';
+----------------------------------------------------------------------------------------------------------------------------------------------+
| Grants for hive@ip-172-31-6-157.us-west-2.compute.internal                                                                                   |
+----------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hive'@'ip-172-31-6-157.us-west-2.compute.internal' IDENTIFIED BY PASSWORD '*4DF1D66463C18D44E3B001A8FB1BBFBEA13E27FC' |
| GRANT ALL PRIVILEGES ON `metastore`.* TO 'hive'@'ip-172-31-6-157.us-west-2.compute.internal'                                                 |
+----------------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> SHOW GRANTS for 'oozie'@'ip-172-31-6-157.us-west-2.compute.internal';
+-----------------------------------------------------------------------------------------------------------------------------------------------+
| Grants for oozie@ip-172-31-6-157.us-west-2.compute.internal                                                                                   |
+-----------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'oozie'@'ip-172-31-6-157.us-west-2.compute.internal' IDENTIFIED BY PASSWORD '*2B03FE0359FAD3B80620490CE614F8622E0828CD' |
| GRANT ALL PRIVILEGES ON `oozie`.* TO 'oozie'@'ip-172-31-6-157.us-west-2.compute.internal'                                                     |
+-----------------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

Command and output for hdfs dfs -ls /user
[root@ip-172-31-6-157 cloudera-scm-server]# hadoop fs -ls /user
Found 7 items
drwxr-xr-x   - hdfs   supergroup          0 2016-09-23 12:06 /user/christie
drwxr-xr-x   - hdfs   supergroup          0 2016-09-23 12:01 /user/hdfs
drwxrwxrwx   - mapred hadoop              0 2016-09-23 11:53 /user/history
drwxrwxr-t   - hive   hive                0 2016-09-23 11:54 /user/hive
drwxrwxr-x   - hue    hue                 0 2016-09-23 11:55 /user/hue
drwxrwxr-x   - oozie  oozie               0 2016-09-23 11:55 /user/oozie
drwxr-xr-x   - hdfs   supergroup          0 2016-09-23 12:07 /user/weiner

Command and output for hadoop classpath
[root@ip-172-31-6-157 cloudera-scm-server]# hadoop classpath
/etc/hadoop/conf:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop/lib/*:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop/.//*:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop-hdfs/./:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop-hdfs/lib/*:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop-hdfs/.//*:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop-yarn/lib/*:/opt/cloudera/parcels/CDH-5.7.3-1.cdh5.7.3.p0.5/lib/hadoop/libexec/../../hadoop-yarn/.//*:/opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/lib/*:/opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/.//*
