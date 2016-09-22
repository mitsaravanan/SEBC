# TeraGen

sudo -u hdfs time hadoop jar /opt/cloudera/parcels/CDH-5.8.0-1.cdh5.8.0.p0.42/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teragen -D dfs.block.size=32000000 10000000 /tmp/mitsaravanan/teragen

Output:

```sh
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=244584
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=167
                HDFS: Number of bytes written=1000000000
                HDFS: Number of read operations=8
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Job Counters
                Launched map tasks=2
                Other local map tasks=2
                Total time spent by all maps in occupied slots (ms)=18261
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=18261
                Total vcore-seconds taken by all map tasks=18261
                Total megabyte-seconds taken by all map tasks=18699264
        Map-Reduce Framework
                Map input records=10000000
                Map output records=10000000
                Input split bytes=167
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=160
                CPU time spent (ms)=21290
                Physical memory (bytes) snapshot=736813056
                Virtual memory (bytes) snapshot=3153240064
                Total committed heap usage (bytes)=786432000
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=21472776955442690
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=1000000000
5.88user 0.25system 0:20.92elapsed 29%CPU (0avgtext+0avgdata 187576maxresident)k
0inputs+1816outputs (0major+32730minor)pagefaults 0swaps
```

# Terasort


time sudo -u hdfs  hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar terasort /tmp/mitsaravanan/terasoft /tmp/mitsaravanan/terasort

output:

```sh
16/09/22 00:26:07 INFO mapreduce.Job: Job job_1474473537399_0029 completed successfully
16/09/22 00:26:08 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=439894966
                FILE: Number of bytes written=879034775
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1000003648
                HDFS: Number of bytes written=1000000000
                HDFS: Number of read operations=120
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=16
        Job Counters
                Launched map tasks=32
                Launched reduce tasks=8
                Data-local map tasks=32
                Total time spent by all maps in occupied slots (ms)=207202
                Total time spent by all reduces in occupied slots (ms)=76533
                Total time spent by all map tasks (ms)=207202
                Total time spent by all reduce tasks (ms)=76533
                Total vcore-seconds taken by all map tasks=207202
                Total vcore-seconds taken by all reduce tasks=76533
                Total megabyte-seconds taken by all map tasks=212174848
                Total megabyte-seconds taken by all reduce tasks=78369792
        Map-Reduce Framework
                Map input records=10000000
                Map output records=10000000
                Map output bytes=1020000000
                Map output materialized bytes=434189915
                Input split bytes=3648
                Combine input records=0
                Combine output records=0
                Reduce input groups=10000000
                Reduce shuffle bytes=434189915
                Reduce input records=10000000
                Reduce output records=10000000
                Spilled Records=20000000
                Shuffled Maps =256
                Failed Shuffles=0
                Merged Map outputs=256
                GC time elapsed (ms)=2733
                CPU time spent (ms)=156160
                Physical memory (bytes) snapshot=18114854912
                Virtual memory (bytes) snapshot=63547236352
                Total committed heap usage (bytes)=20964704256
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1000000000
        File Output Format Counters
                Bytes Written=1000000000
16/09/22 00:26:08 INFO terasort.TeraSort: done
8.49user 0.32system 1:03.35elapsed 13%CPU (0avgtext+0avgdata 194228maxresident)k
16inputs+1896outputs (0major+37142minor)pagefaults 0swaps
```

# Teravalidate:

time sudo -u hdfs hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar teravalidate /tmp/mitsaravanan/terasoft /tmp/mitsaravanan/teravalidate

output:

```sh
16/09/22 00:30:27 INFO mapreduce.Job: Counters: 35
        File System Counters
                FILE: Number of bytes read=228103127
                FILE: Number of bytes written=456446985
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1000000228
                HDFS: Number of bytes written=0
                HDFS: Number of read operations=6
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=0
        Job Counters
                Failed map tasks=4
                Killed reduce tasks=1
                Launched map tasks=6
                Other local map tasks=4
                Data-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=41066
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=41066
                Total vcore-seconds taken by all map tasks=41066
                Total megabyte-seconds taken by all map tasks=42051584
        Map-Reduce Framework
                Map input records=10000000
                Map output records=5000363
                Map output bytes=515036935
                Map output materialized bytes=228098478
                Input split bytes=228
                Combine input records=0
                Spilled Records=10000726
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=541
                CPU time spent (ms)=31200
                Physical memory (bytes) snapshot=1299537920
                Virtual memory (bytes) snapshot=3156918272
                Total committed heap usage (bytes)=1427111936
        File Input Format Counters
                Bytes Read=1000000000
6.15user 0.26system 0:28.41elapsed 22%CPU (0avgtext+0avgdata 183820maxresident)k
0inputs+1816outputs (0major+36580minor)pagefaults 0swaps

real    0m28.424s
user    0m6.165s
sys     0m0.270s
```
# CacheAdmin Commands:

```sh
sudo -u hdfs hdfs cacheadmin -addPool cache_pool
sudo -u hdfs hdfs cacheadmin -addDirective -path /user/hduser -pool cache_pool
sudo -u hdfs hdfs cacheadmin -listPools -stats cache_pool

[ec2-user@ip-172-31-1-193 parcels]$  sudo -u hdfs hdfs cacheadmin -addPool cache_pool
Successfully added cache pool cache_pool.
[ec2-user@ip-172-31-1-193 parcels]$ sudo -u hdfs hdfs cacheadmin -addDirective -path /user/hduser -pool cache_pool
Added cache directive 1
[ec2-user@ip-172-31-1-193 parcels]$ sudo -u hdfs hdfs cacheadmin -listPools -stats cache_pool
Found 1 result.
NAME        OWNER  GROUP  MODE            LIMIT  MAXTTL  BYTES_NEEDED  BYTES_CACHED  BYTES_OVERLIMIT  FILES_NEEDED  FILES_CACHED
cache_pool  hdfs   hdfs   rwxr-xr-x   unlimited   never             0             0                0             0             0
[ec2-user@ip-172-31-1-193 parcels]$
```