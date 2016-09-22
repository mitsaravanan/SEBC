[ec2-user@ip-172-31-1-193 hdfs]$ kinit mitsaravanan

[ec2-user@ip-172-31-1-193 hdfs]$ hadoop fs -ls /user
Found 6 items
drwx------   - hdfs         supergroup            0 2016-09-21 09:59 /user/hdfs
drwxrwxrwx   - mapred       hadoop                0 2016-09-21 00:16 /user/history
drwxrwxr-t   - hive         hive                  0 2016-09-21 00:20 /user/hive
drwxrwxr-x   - hue          hue                   0 2016-09-21 00:21 /user/hue
drwxr-xr-x   - mitsaravanan mitsaravanan          0 2016-09-22 14:27 /user/mitsravanan
drwxrwxr-x   - oozie        oozie                 0 2016-09-21 00:28 /user/oozie
[ec2-user@ip-172-31-1-193 hdfs]$ hadoop fs -ls /user/mitsravanan
[ec2-user@ip-172-31-1-193 hdfs]$ klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: mitsaravanan@MITSARAVANAN.COM

Valid starting       Expires              Service principal
09/22/2016 14:28:07  09/23/2016 14:28:07  krbtgt/MITSARAVANAN.COM@MITSARAVANAN.COM
        renew until 09/29/2016 14:28:07


