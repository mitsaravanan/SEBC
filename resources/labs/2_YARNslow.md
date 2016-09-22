# Slowest run yarn job
container memory - 512 1024 
```sh
+ for i in 2
+ for j in 2
+ for k in 512 1024
echo "($k*0.8)/1" | bc
++ echo '(512*0.8)/1'
++ bc
+ MAP_MB=409
echo "($k*0.8)/1" | bc
++ echo '(512*0.8)/1'
++ bc
+ RED_MB=409
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapreduce.job.maps=2 -Dmapreduce.map.memory.mb=512 -Dmapreduce.map.java.opts.max.heap=409 100000 /results/tg-10GB-2-2-512
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar terasort -Dmapreduce.job.maps=2 -Dmapreduce.job.reduces=2 -Dmapreduce.map.memory.mb=512 -Dmapreduce.map.java.opts.max.heap=409 -Dmapreduce.reduce.memory.mb=512 -Dmapreduce.reduce.java.opts.max.heap=409 /results/tg-10GB-2-2-512 /results/ts-10GB-2-2-512
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/tg-10GB-2-2-512
Deleted /results/tg-10GB-2-2-512
+ sudo -u hdfs /opt/cloudera/parcels/CDH/bin/hadoop fs -rm -r -skipTrash /results/ts-10GB-2-2-512
Deleted /results/ts-10GB-2-2-512
+ for k in 512 1024
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

echo Testing loop ended on `date`
date
++ date
+ echo Testing loop ended on Thu Sep 22 10:19:09 EDT 2016
Testing loop ended on Thu Sep 22 10:19:09 EDT 2016

real    1m28.407s
user    0m40.643s
sys     0m1.779s
```