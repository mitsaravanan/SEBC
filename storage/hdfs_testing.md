<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---
<div style="page-break-after: always;"></div>

# <center> <a name="hdfs_section"/>HDFS<p>

* Review and reinforcement
* HDFS Basics
    * <a href="#hdfs_namenode_ha">NameNode HA</a>
    * <a href="#hdfs_benchmarking">Benchmarking</a>
    * <a href="#hdfs_c5">HDFS & C5</a>    

---
<div style="page-break-after: always;"></div>

## <center>Notes on Service Deployment</center>

* [Practical advice on field deployment](http://blog.cloudera.com/blog/2015/01/how-to-deploy-apache-hadoop-clusters-like-a-boss/)
* Design principles for deployment 
    * Separation of concerns
    * Preparing for security
* Cloudera uses four role types to guide deployment 
    * Utility nodes for cluster administration
    * Master nodes control executive and supervisory processes
    * Worker nodes provide storage and processing resources
    * Edge: Client access, data ingestion, security perimeter

---
<div style="page-break-after: always;"></div>

## <center>Node count alters the architecture

* <10 nodes: combine master & workers, utility & edge roles 
* 20-100 nodes: masters and workers separated, dedicated utility & edge node
* 100+ nodes: more utility, master, and edge machines depending on use case
* As roles separate, focus on differences in resources
    * Four disks, RAID OS volume on master nodes
    * More RAM and spindles on worker nodes
    * VMs for edge/utility roles

---
<div style="page-break-after: always;"></div>


## <center> <a name="hdfs_namenode_ha"/> NameNode HA

* CM 5 offers a [NameNode HA wizard](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Managing-Clusters/cm5mc_hdfs_hi_avail.html)
    * `HDFS -> Actions -> Enable High Availability`
    * [Place the Journal Quorum Managers](http://www.cloudera.com/documentation/enterprise/latest/topics/cdh_hag_hdfs_ha_enabling.html#cmug_topic_5_12_1)
    * [Understand Zookeeper's role] (https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithQJM.html)

---
<div style="page-break-after: always;"></div>

## <center> <a name="hdfs_benchmarking"/> Benchmarking

* Following installation, we test for hardware and network problems
* Common tools used in the field
    * [TeraSort Suite: teragen, terasort, teravalidate](http://www.michael-noll.com/blog/2011/04/09/benchmarking-and-stress-testing-an-hadoop-cluster-with-terasort-testdfsio-nnbench-mrbench/#terasort-benchmark-suite)
    * A few use [TestDFSIO](http://www.michael-noll.com/blog/2011/04/09/benchmarking-and-stress-testing-an-hadoop-cluster-with-terasort-testdfsio-nnbench-mrbench/#testdfsio)
* Consider testing the NameNode too: [nnbench](http://www.michael-noll.com/blog/2011/04/09/benchmarking-and-stress-testing-an-hadoop-cluster-with-terasort-testdfsio-nnbench-mrbench/#namenode-benchmark-nnbench)

---
<div style="page-break-after: always;"></div>

## <center> <a name="hdfs_c5"/> C5 Goals for HDFS

Strategy for storage in C5:

* Plan for larger RAM complements
* Perform faster backups
* Provide more data recovery options
* Provide more client access options

---
<div style="page-break-after: always;"></div>

## <center> Key HDFS Features in C5

* <a href="#hdfs_dir_caching">Directory caching </a> 
* <a href="#hdfs_dir_snapshots"> Directory snapshots </a>
* <a href="#nfs_gateway"> NFS Gateway</a>
* <a href="#hdfs_backups"/>Backups

---
<div style="page-break-after: always;"></div>

## <center> <a name="hdfs_dir_caching"/> Directory caching: Use case
### <center> Repeating a query (cache effect)

<img src="http://blog.cloudera.com/wp-content/uploads/2014/08/hdfs-cache-f1.jpg">

---
<div style="page-break-after: always;"></div>

## <center> Problem: Performance on Repeated Queries

* The NameNode links file paths to block locations on the DataNodes
    * Locality is defined by [local disk storage only](https://issues.apache.org/jira/browse/HDFS-4949)
* A repeated query might pay the same disk I/O cost as the first query
    * Not a big cost to MapReduce jobs
    * For near real-time use cases, it is expensive
    
---
<div style="page-break-after: always;"></div>

## <center> Solution: [HDFS Read Caching](http://blog.cloudera.com/blog/2014/08/new-in-cdh-5-1-hdfs-read-caching/)
    
Adds cache locality to NN reports<p>

* You can specify an HDFS file/directory you want cached
* The affected DataNodes receive the cache instruction on read
    * Blocks are then cached up to the file's replica limit
    * In-memory storage is off-heap: no heavy impact on DataNodes
* A data-local client, such as `impalad`, can further exploit locality
    * Short-circuit read (SCR) API
    * Zero-copy read (ZCR) API

---
<div style="page-break-after: always;"></div>

## <center> Directory caching: Implementation<p>

<center><img src="http://www.cloudera.com/documentation/enterprise/latest/images/caching.png" height="325" width="400"></center>

---
<div style="page-break-after: always;"></div>

## <center> Directory caching: Roles and responsibilities

* HDFS admin `hdfs cacheadmin` command
    * Create a cache pool (needed to enforce quotas)
    * Assign directives (paths to cache)
    * List statistics on hit rate, memory consumed, etc.
    * Amend pools & directives as needed
* DataNodes
    * Track blocks in system memory 
    * Report cache state to NameNode
* Job client
    * Queries NN for DNs with cached blocks

---
<div style="page-break-after: always;"></div>

## <center> Directory caching: Other notes

* [Caching documentation is here] (http://www.cloudera.com/documentation/enterprise/latest/topics/cdh_ig_hdfs_caching.html)
* We do have to balance memory demand for caching with other memory-based features
    * Impala users have ["NRT" expectations](http://stackoverflow.com/questions/5267231/what-is-the-definition-of-realtime-near-realtime-and-batch-give-examples-of-ea)
    * So do HBase and Search applications
    * We'll discuss this further with YARN and resource management
    
---     
<div style="page-break-after: always;"></div>

## <center> <a name="scr_and_zcr"/> Technical Notes on SCR and ZCR

* General advice: take time to map key upstream features to their [JIRAs] (https://issues.apache.org/jira)
* [Short-circuit Reads] (https://issues.apache.org/jira/browse/HDFS-2246)
    * Clients can examine a DataNode's process map to find cached blocks
    * Based on [file descriptor passing](http://poincare.matf.bg.ac.rs/~ivana/courses/tos/sistemi_knjige/pomocno/apue/APUE/0201433079/ch17lev1sec4.html), AKA short-circuit reads.
    * [Enabled in CM by default](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/admin_hdfs_short_circuit_reads.html) 
* There is also zero-copy Read
    * [Uses `mmap()` to read system page$](https://issues.apache.org/jira/browse/HDFS-4953)
    * Clients can implement the [API](https://issues.apache.org/jira/browse/HDFS-5191) 
* Other JIRAs on the roadmap
    * Write caching: [HDFS-5851](https://issues.apache.org/jira/browse/HDFS-5851)

---    
<div style="page-break-after: always;"></div>

## <center> <a name="hdfs_dir_snapshots"/> HDFS Snapshots

* Users with write permissions on a directory may retrieve a deleted file
    * Easy to track changes to a directory over time
    * Employs [copy-on-write](http://en.wikipedia.org/wiki/Copy-on-write) technique to track with DN block location + timestamp 
    * Deleted files may be retrieved from a version folder
    * Like `.Trash` foldeir without a time-based expiration
* [Apache docs on the CLI](http://archive.cloudera.com/cdh5/cdh/5/hadoop/hadoop-project-dist/hadoop-hdfs/HdfsSnapshots.html) 
* [Using snapshots in Cloudera Manager] (http://www.cloudera.com/documentation/enterprise/latest/topics/cm_bdr_snapshot_intro.html) requires an active trial or Enterprise license

---
<div style="page-break-after: always;"></div>

## <center> <a name="hdfs_backups"/> HDFS Backups

* In Cloudera Manager, called BDR (Backup and Data Recovery)
* Central services for managing backups and replications
    * Configuration, monitoring, alerting
    * Uses snapshot & replication features
    * Executes `distCp` jobs
    * Will preserves file attributes and other metadata
 
---
<div style="page-break-after: always;"></div>

## <center> <a name="nfs_gateway"/> NFS Gateway

* Linux NFSv3 service ported to HDFS
    * Supports Windows-based browsing, file transfers 
    * Alternative to webHDFS or httpfs
* Any NFS-capable HDFS client can be an NFS gateway
* Properties configured in `hdfs-site.xml`
* Relies on Linux rpcbind/portmapper services
    * See [HDFS-4763](https://issues.apache.org/jira/browse/HDFS-4763)

---
<div style="page-break-after: always;"></div>

## <center> HDFS Problems/Diagnoses/Solutions

### <center>HDFS Labs Overview

* Before you start, create an Issue called Storage labs
    * Add the Lab milestone
    * Label the issue as `Started`
    * Assign yourself to the Issue
* The following labs will have you:
    * Replicate data to another cluster
    * Use `teragen` and `terasort` to benchmark performance
    * Enable HA for the NameNode

---
<div style="page-break-after: always;"></div>

## <center> HDFS Lab: Replicate to another cluster

Note: actual data replication in the cloud depends on two clusters
that are local to each other. If your partner's cluster is remote
to your, you may not transfer any data from your partner's cluster,
even if you get the job to start.

* Choose a partner in class
* Name a source directory using your GitHub handle
* Name a target directory using your partner's GitHub handle
* Use `teragen` to create a 500 MB file
* Replicate your partner's file to the target directory you made for them 
* Using the HDFS Browser in Cloudera Manager
    * Get a screenshot that lists your partner's target directory
    * Store this image in `storage/labs/0_partnerGitHub_yourGitHub.png`

---
<div style="page-break-after: always;"></div>

## <center> HDFS Lab: Test HDFS performance

* Create a ~10 GB file using `teragen`
    * Set the block size to 32 MB for this file
    * Use the `time` command to record the job duration
* Run the `terasort` command against this file twice
    * Use the `time` command to capture each run's duration
    * Create a cache pool and directive for the teragen output before the first run
* Record your work, including:
    * The `teragen` command you used to create your test file
    * The commands you used to configure HDFS caching
    * The `time` output for each job run
* Store and comment on these outputs in `storage/labs/1_terasort_tests.md` 

---
<div style="page-break-after: always;"></div>

## <center> HDFS Lab: Enable HDFS HA

* Use the Cloudera Manager wizard to enable HA
    * Once configured, get a screenshot of the HDFS Instances tab
        * Name the file `storage/2_HDFS_HA.png` 
* Add a CM user and name it with your GitHub handle
    * Assign the `Full Administrator` role to this user
    * Assign the password `cloudera` to this user
    * Re-assign the 'admin' user to the `Limited Operator` role
    * Take a screenshot of your users page; save it to `storage/labs/3_CM_users.png`
