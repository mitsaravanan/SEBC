# PI example using weiner

```sh

[ec2-user@ip-172-31-6-157 hadoop-mapreduce]$ hadoop jar hadoop-mapreduce-examples-2.6.0-cdh5.7.3.jar pi 2 100000
Number of Maps  = 2
Samples per Map = 100000
Wrote input for Map #0
Wrote input for Map #1
Starting Job
16/09/23 14:06:47 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-6-153.us-west-2.compute.internal/172.31.6.153:8032
16/09/23 14:06:47 INFO hdfs.DFSClient: Created token for weiner: HDFS_DELEGATION_TOKEN owner=weiner@MITSARAVANAN.NYC, renewer=yarn, realUser=, issueDate=1474654007325, maxDate=1475258807325, sequenceNumber=1, masterKeyId=2 on 172.31.6.157:8020
16/09/23 14:06:47 INFO security.TokenCache: Got dt for hdfs://ip-172-31-6-157.us-west-2.compute.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.6.157:8020, Ident: (token for weiner: HDFS_DELEGATION_TOKEN owner=weiner@MITSARAVANAN.NYC, renewer=yarn, realUser=, issueDate=1474654007325, maxDate=1475258807325, sequenceNumber=1, masterKeyId=2)
16/09/23 14:06:47 INFO input.FileInputFormat: Total input paths to process : 2
16/09/23 14:06:47 INFO mapreduce.JobSubmitter: number of splits:2
16/09/23 14:06:47 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1474649188867_0001
16/09/23 14:06:47 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 172.31.6.157:8020, Ident: (token for weiner: HDFS_DELEGATION_TOKEN owner=weiner@MITSARAVANAN.NYC, renewer=yarn, realUser=, issueDate=1474654007325, maxDate=1475258807325, sequenceNumber=1, masterKeyId=2)
16/09/23 14:06:48 INFO impl.YarnClientImpl: Submitted application application_1474649188867_0001
16/09/23 14:06:48 INFO mapreduce.Job: The url to track the job: http://ip-172-31-6-153.us-west-2.compute.internal:8088/proxy/application_1474649188867_0001/
16/09/23 14:06:48 INFO mapreduce.Job: Running job: job_1474649188867_0001
16/09/23 14:06:56 INFO mapreduce.Job: Job job_1474649188867_0001 running in uber mode : false
16/09/23 14:06:56 INFO mapreduce.Job:  map 0% reduce 0%
16/09/23 14:07:04 INFO mapreduce.Job:  map 100% reduce 0%
16/09/23 14:07:10 INFO mapreduce.Job:  map 100% reduce 100%
16/09/23 14:07:10 INFO mapreduce.Job: Job job_1474649188867_0001 completed successfully
16/09/23 14:07:11 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=52
                FILE: Number of bytes written=362767
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=596
                HDFS: Number of bytes written=215
                HDFS: Number of read operations=11
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Job Counters
                Launched map tasks=2
                Launched reduce tasks=1
                Data-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=12114
                Total time spent by all reduces in occupied slots (ms)=3165
                Total time spent by all map tasks (ms)=12114
                Total time spent by all reduce tasks (ms)=3165
                Total vcore-seconds taken by all map tasks=12114
                Total vcore-seconds taken by all reduce tasks=3165
                Total megabyte-seconds taken by all map tasks=12404736
                Total megabyte-seconds taken by all reduce tasks=3240960
        Map-Reduce Framework
                Map input records=2
                Map output records=4
                Map output bytes=36
                Map output materialized bytes=70
                Input split bytes=360
                Combine input records=0
                Combine output records=0
                Reduce input groups=2
                Reduce shuffle bytes=70
                Reduce input records=4
                Reduce output records=0
                Spilled Records=8
                Shuffled Maps =2
                Failed Shuffles=0
                Merged Map outputs=2
                GC time elapsed (ms)=60
                CPU time spent (ms)=2040
                Physical memory (bytes) snapshot=1092382720
                Virtual memory (bytes) snapshot=4777664512
                Total committed heap usage (bytes)=1226833920
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=236
        File Output Format Counters
                Bytes Written=97
Job Finished in 23.93 seconds
Estimated value of Pi is 3.14118000000000000000
```