# Fastest run yarn job
container memory - 1024 8192
```sh
echo "($k*0.8)/1" | bc
++ echo '(1024*0.8)/1'
++ bc
+ MAP_MB=819
echo "($k*0.8)/1" | bc
++ echo '(1024*0.8)/1'
++ bc
+ RED_MB=819
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapreduce.job.maps=2 -Dmapreduce.map.memory.mb=1024 -Dmapreduce.map.java.opts.max.heap=819 100000 /results/tg-10GB-2-2-1024
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar terasort -Dmapreduce.job.maps=2 -Dmapreduce.job.reduces=2 -Dmapreduce.map.memory.mb=1024 -Dmapreduce.map.java.opts.max.heap=819 -Dmapreduce.reduce.memory.mb=1024 -Dmapreduce.reduce.java.opts.max.heap=819 /results/tg-10GB-2-2-1024 /results/ts-10GB-2-2-1024
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/tg-10GB-2-2-1024
Deleted /results/tg-10GB-2-2-1024
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/ts-10GB-2-2-1024
Deleted /results/ts-10GB-2-2-1024
+ for k in 1024 8192
echo "($k*0.8)/1" | bc
++ echo '(8192*0.8)/1'
++ bc
+ MAP_MB=6553
echo "($k*0.8)/1" | bc
++ echo '(8192*0.8)/1'
++ bc
+ RED_MB=6553
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapreduce.job.maps=2 -Dmapreduce.map.memory.mb=8192 -Dmapreduce.map.java.opts.max.heap=6553 100000 /results/tg-10GB-2-2-8192
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar terasort -Dmapreduce.job.maps=2 -Dmapreduce.job.reduces=2 -Dmapreduce.map.memory.mb=8192 -Dmapreduce.map.java.opts.max.heap=6553 -Dmapreduce.reduce.memory.mb=8192 -Dmapreduce.reduce.java.opts.max.heap=6553 /results/tg-10GB-2-2-8192 /results/ts-10GB-2-2-8192
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/tg-10GB-2-2-8192
Deleted /results/tg-10GB-2-2-8192
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/ts-10GB-2-2-8192
rm: `/results/ts-10GB-2-2-8192': No such file or directory

echo Testing loop ended on `date`
date
++ date
+ echo Testing loop ended on Thu Sep 22 10:27:08 EDT 2016
Testing loop ended on Thu Sep 22 10:27:08 EDT 2016

real    1m0.166s
user    0m36.572s
sys     0m1.634s
```