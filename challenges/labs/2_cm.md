```sh
[root@ip-172-31-6-157 yum.repos.d]# ls -ltr
total 36
-rw-r--r--. 1 root root  358 Nov  9  2015 redhat.repo
-rw-r--r--. 1 root root 1440 Sep 12 08:41 mysql-community-source.repo
-rw-r--r--. 1 root root  290 Sep 22 15:45 cloudera-manager.repo
-rw-r--r--. 1 root root 8679 Sep 23 08:18 redhat-rhui.repo
-rw-r--r--. 1 root root   80 Sep 23 08:18 rhui-load-balancers.conf
-rw-r--r--. 1 root root  607 Sep 23 08:18 redhat-rhui-client-config.repo
-rw-r--r--. 1 root root 1416 Sep 23 09:48 mysql-community.repo


CREATE USER 'cm'@'ip-172-31-6-157.us-west-2.compute.internal' IDENTIFIED BY 'cm';
grant all privileges on cm.* to 'cm'@'ip-172-31-6-157.us-west-2.compute.internal' identified by 'cm';

[root@ip-172-31-6-157 cloudera-scm-server]# head -1 /var/log/cloudera-scm-server/cloudera-scm-server.log
2016-09-23 10:40:27,475 INFO main:com.cloudera.server.cmf.Main: Starting SCM Server. JVM Args: [-Dlog4j.configuration=file:/etc/cloudera-scm-server/log4j.properties, -Dfile.encoding=UTF-8, -Dcmf.root.logger=INFO,LOGFILE, -Dcmf.log.dir=/var/log/cloudera-scm-server, -Dcmf.log.file=cloudera-scm-server.log, -Dcmf.jetty.threshhold=WARN, -Dcmf.schema.dir=/usr/share/cmf/schema, -Djava.awt.headless=true, -Djava.net.preferIPv4Stack=true, -Dpython.home=/usr/share/cmf/python, -XX:+UseConcMarkSweepGC, -XX:+UseParNewGC, -XX:+HeapDumpOnOutOfMemoryError, -Xmx2G, -XX:MaxPermSize=256m, -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath=/tmp, -XX:OnOutOfMemoryError=kill -9 %p], Args: [], Version: 5.8.2 (#17 built by jenkins on 20160916-1419 git: d23c620f3a3bbd85d8511d6ebba49beaaab14b75)
[root@ip-172-31-6-157 cloudera-scm-server]#

[root@ip-172-31-6-157 cloudera-scm-server]# grep "Started Jetty server" /var/log/cloudera-scm-server/cloudera-scm-server.log
2016-09-23 10:41:32,488 INFO WebServerImpl:com.cloudera.server.cmf.WebServerImpl: Started Jetty server.

```