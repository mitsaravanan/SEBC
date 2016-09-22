**mapreduce.jobs.maps calculation**

```sh
$ yarn.nodemanager.resource.memory-mb	    111616
$ mapreduce.map.memory.mb	                1024
$ yarn.nodemanager.resource.cpu-vcores  	64
$ mapreduce.map.cpu.vcores	                1
$ number of physical drives	                12
$ workload factor	                        2
$ number of worker nodes	                10
```
```sh
$ mapreduce.jobs.maps=MIN(yarn.nodemanager.resource.memory-mb / mapreduce.map.memory.mb,yarn.nodemanager.resource.cpu-vcores / mapreduce.map.cpu.vcores, number of physical drives x workload factor) x number of worker nodes
$ mapreduce.jobs.maps=240