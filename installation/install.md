<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---

## <center> <a name="cm_cdh_installation_section"/>Cloudera Manager & CDH Installation

* <a href="#install_methods">Installation Methods</a>
* <a href="#parcels">Understanding Parcels</a>
* <a href="#db_setup">Embedded vs. external database</a>
* <a href="#cm_cdh_key_points">Supplemental CM/DH Points</a>
* <a href="#cm_ui_overview">Cloudera Manager UI Overview</a>

---
<div style="page-break-after: always;"></div>

## <center> <a name="install_methods"/> CM/CDH Installation

* We use Cloudera  Manager to:
    * Monitor host status (via an agent process)
    * Organize CDH clusters, deploy services
    * Set and observe service configuration
    * Automate common tasks: HA NameNode, Kerberos integration

---
<div style="page-break-after: always;"></div>

## <center> Cloudera Manager architecture

<center> <img src="http://www.cloudera.com/content/cloudera/en/documentation/core/latest/images/cm_arch.png"> </center>

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_install_paths"/>Installation paths

* [Path A: One-stop binary installer](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_install_path_a.html)
    * Used for short-term, throwaway projects
    * Embedded, hard-configured PostgreSQL server
* [Path B: Install CM and database manually](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_install_path_b.html)
    * Any cluster meant to run more than 3-6 months
    * Supports Oracle, MySQL, and PostgreSQL servers
    * Can deploy CDH with Linux packages or [Parcels](http://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_parcels.html)
* [Path C: Tarballs](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_install_path_c.html)
    * Useful if privileged access is not available
    * Let other deployment tools drive
    * Don't need Cloudera Manager

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_install_logging"/>Installation Milestones with Path A []()

* Conducts one Linux configuration check (SELinux disabled)
* Installs package repos for
   * Dedicated PostgreSQL
   * Cloudera Manager (includes supported JDK)
* Installs Oracle JDK, PostgreSQL, and CM
* Adds hosts, deploys clusters
  * Many configurations are done for you

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_install_milestones"/> Typical Path B Milestones []()

* Review hardware, OS, disk, and network/kernel settings
* Install Oracle JDK
    * Available in Cloudera Manager's package repo
    * OpenJDK is not supported by Cloudera
* Install [database server](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_installing_configuring_dbs.html?scroll=cmig_topic_5_2_unique_1#cmig_topic_5_1_unique_1)
  * Use MySQL, Oracle, or PostgreSQL
* Install the CM server and agent packages
    * Accessing MySQL via CM requires a JDBC connector
* CM will
  * Distribute agent software
  * Distribute CDH software
  * Deploy and activate CDH services<p>

---
<div style="page-break-after: always;"></div>

## <center> <a name="parcels"/> Installing CDH with Parcels

Parcels are [distribution modules specific to CM](https://github.com/cloudera/cm_ext/wiki/Parcels:-What-and-Why%3F)

* Cloudera's core components in one distribution
    * Additional parcels for other components
* Simpler to manage than Linux packages
    * Default path: <code>/opt/cloudera/parcels</code>
    * Easy to create/maintain local parcel repos
* Most components bind to CM through [Custom Service Descriptors](https://github.com/cloudera/cm_ext/wiki/CSD-Overview)
* Structure is a tarball, more or less, with [some manifest and layout rules](https://github.com/cloudera/cm_ext/wiki/Building-a-parcel)
    * Content list is stored in <code>meta/parcel.json</code>
    * Clients can check integrity via a <code>manifest.json</code> file kept on the repo server

---
<div style="page-break-after: always;"></div>

## <center> Parcel Lifecycle</p>

<center> <img src="http://blog.cloudera.com/wp-content/uploads/2013/05/parcels1.png"> </center>

* [How to manage parcels](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Installation-Guide/cm5ig_parcels.html)

---
<div style="page-break-after: always;"></div>

## <center> Parcels Lifecycle

* Lifecycle actions
    * Download
    * Distribute
    * Activate/deactivate
    * Remove
    * Delete<p/>
* The path <code>/opt/cloudera/parcels/CDH</code> points to the active parcel's directory

---
<div style="page-break-after: always;"></div>

## <center> <a name="db_setup"/>Setting up the database

* <a href="#cm_service_dbs">Management/CDH services that use a database</a>
* <a href="#cm_replicate_db">CM database replication for HA</a>

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_service_dbs"/>[Databases and Other Stores](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_installing_configuring_dbs.html)

* Management Services (per CM instance)
    * Reports Manager
    * Navigator Audit & Metadata Servers (not covered this week)
    * Host and Service Monitors use  [LevelDB](https://github.com/google/leveldb) implementations
* CDH Services
    * Hive Metastore
    * Sentry
    * [Oozie](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_mc_oozie_service.html#cmig_topic_14_unique_1)
    * [Hue](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_mc_hue_service.html#cmig_topic_15_unique_1)

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_replicate_db"/> MySQL Replication for HA </a></p>

* Configuring Cloudera Manager for active-passive HA [is non-trivial](https://www.cloudera.com/documentation/enterprise/latest/topics/admin_cm_ha_overview.html#concept_bhl_cvc_pr)
  * Requires a load balancer
  * Highly-available networked storage
  * Supported Heartbeat Demon software

* For lab, we'll only [install a MySQL server and a replica](http://dev.mysql.com/doc/refman/5.5/en/replication-howto.html)

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_ui_overview"/>Path A Install Screen

<center> <img src="png/CM5_Installer_Screen.png"/>

---
<div style="page-break-after: always;"></div>

## <center> CM Install Labs - *Before* You Start

* Create a private repo in your GitHub account
    * In the Settings tab, enable the Issues feature
    * Add instructors as Collaborators (`mfernest`, `mikeridley`)
* Submit work as Markdown docs or PNG files
    * At a minimum, use code style to present text output
* Create an Issue in your repo called `Installation Lab`
     * Add it to the `Labs` milestone
     * Assign the label `Started`
* Use each Issue to track your progress, describe problems, document solutions

---
<div style="page-break-after: always;"></div>

## <center> CM Install Lab

* You can AWS or GCE via Cloudcat
* With AWS, create five `m3.xlarge` nodes
  * Do not use spot instances
* With GCE, create five `n1-highmen-2` nodes
  * Do not use preemptible instances
* One instance can host the Cloudera Manager server, Management Services, and edge roles
* Verify you've chosen a [Cloudera-supported OS](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_cm_requirements.html)

---
<div style="page-break-after: always;"></div>

## <center> CM Install Labs - Path B Installation Overview

* Add your node names & IP addresses to `installation/0_nodeIPs.md`
* Document your configuration checks in `installation/1_preinstall.md`
* Install a MySQL server and replica
* Install the latest available releases of CM & CDH
* <a href="#parcels_repo_lab">Bonus: create a Parcels repository</a>

---
<div style="page-break-after: always;"></div>

## <center> CM Install Lab
## <center> <a name="linux_config_lab"/>Linux Configuration Checks

The checklist below is a brief list [of essential system
settings](http://tiny.cloudera.com/7steps). A typical engagement
checklist is much more detailed

Review the checks below. In each case, use a command to show the
current value of each property. Also show the command you used to
modify any property as needed.

Capture this work in the file `installation/1_prechecks.md`.  Check
each node, but report the results only one of them.

1. Check `vm.swappiness` on all your nodes
    * Set the value to `1` if necessary
2. Check that `noatime` is set on any non-root volumes you have
3. Check that the reserve space of any non-root volumes to `0`
4. Check the user limits for maximum file descriptors and processes
5. Test forward and reverse host lookups for correct resolution
6. Verify/enable the <code>nscd</code> service
7. Verify/enable the <code>ntpd</code> service<br>

---
<div style="page-break-after: always;"></div>

## <center> MySQL/MariaDB Installation Lab
## <center> <a name="mysql_replication_lab"/>Configure MySQL with a replica server

Choose one of these plans to follow:

**Plan One**: Use the steps [documented here for MariaDB](http://www.cloudera.com/documentation/enterprise/latest/topics/install_cm_mariadb.html) or [here for MySQL](http://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_mysql.html).<br>
**Plan Two**: Use the steps given below for MySQL<br>
**Plan Three**: If you're a database server expert, do your thing.

In your Issue for this lab, indicate which plan you intend to follow.

---
<div style="page-break-after: always;"></div>

## <center> MySQL installation - Plan Two Detail

1. Get MySQL 5.5
    * Use the repo [supported by MySQL](http://dev.mysql.com/downloads/mysql/5.5.html#downloads).
    * Install the <code>mysql</code> package on all nodes
    * Install <code>mysql-server</code> on the server and replica nodes
    * Download and copy [the JDBC connector](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-binary-installation.html) to all nodes. 
2. You should not need to edit your <code>/etc/my.cnf</code> file
    * Consult your MySQL documentation for enabling replication.<p>
3. Start the <code>mysqld</code> service.
4. Use <code>/usr/bin/mysql_secure_installation</code> to:<br>
    a. Set password protection for the server<br>
    b. Revoke permissions for anonymous users<br>
    c. Permit remote privileged login<br>
    d. Remove test databases<br>
    e. Refresh privileges in memory<br>
    f. Refreshes the <code>mysqld</code> service<p>
5. On the master MySQL node, grant replication privileges for your replica node:<br>
    a. Log in with <code>mysql -u ... -p</code> <br>
    b. Note the FQDN of your replica host.<br>
    c. <code>mysql> **GRANT REPLICATION SLAVE ON \*.\* TO '*user*'@'*FQDN*' IDENTIFIED BY '*password*';**</code><br>
    d. <code>mysql> **SET GLOBAL binlog_format = 'ROW';** </code><br>
    e. <code>mysql> **FLUSH TABLES WITH READ LOCK;</code>**<p>
6. In a second terminal session, log into the MySQL master and show its  status:<br>
    a. <code>mysql> **SHOW MASTER STATUS;**</code><br>
    b. Capture the file name and byte offset. The replica uses this info to sync to the master.<br>
    c. Logout and dismiss the second session; remove the lock on the first with <code>mysql> **UNLOCK TABLES;**</code><p>
7. Now log on to the replica. Use the following statements to coneect with the master:<br>
    <code>mysql> **CHANGE MASTER TO**<br> **MASTER_HOST='*master host*',**<br> **MASTER_USER='*replica user*',**<br> **MASTER_PASSWORD='*replica password*',**<br> **MASTER_LOG_FILE='*master file name*',**<br> **MASTER_LOG_POS=*master file offset*;**</code><p>
8. Next, initiate slave operations and confirm replication.<br>
    a. <code>mysql> **START SLAVE;**</code><br>
    b. <code>mysql> **SHOW SLAVE STATUS \G**</code><br>
    c. If successful, the <code>Slave_IO_State</code> field will read <code>Waiting for master to send event</code><br>
    d. Once successful, capture this output and store it in <code>installation/2_replica_working.md</code><br>
    e. Review your log (<code>/var/log/mysqld.log</code>) for errors. If stuck, consult with a colleague or instructor.<p>

---
<div style="page-break-after: always;"></div>

## <center> CM/CDH Install Lab
## <center> Path B using Cloudera 5.8.x

[The full rundown is here](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_ig_install_path_b.html?scroll=cmig_topic_6_6). Ensure the following settings:

* Do not apply Single User Mode. Do not. Don't do it.
* Use only Cloudera's standard repositories
* Ignore all wizard steps that are marked `(Optional)`
* Install the Data Hub Edition
* Install CDH using parcels
* Rename your cluster to match your GitHub name
* Deploy  **only** the `Coreset` of CDH services.
* Be sure to deploy three ZooKeeper instances.
* Once your cluster is healthy, take a screenshot of the home page
    * Name the file `installation/3_cm_installed.png`.
* Mark your Issue 'submitted' if you won't attempt the Bonus lab.

---
<div style="page-break-after: always;"></div>

## <center> Cluster install: Bonus lab
## <center> <a name="parcels_repo_lab"/>Create a local parcel repo (manual)

* Click the parcel indicator in CM's navigation bar
    * Under Settings, note the Remote Parcel Repository URLs value
* Default parcel links include:
    * [Latest CDH5 release](http://archive.cloudera.com/cdh5/parcels/latest)
    * [Latest CDH4 release](http://archive.cloudera.com/cdh4/parcels/latest)
    * Standalone components, such as Accumulo and Kafka
* Follow the [documentation](http://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_create_local_parcel_repo.html)
* Set the new repository location in Cloudera Manager
* Capture this setting in a screenshot and save it to `installation/4_local_repo.png`
* Mark your Issue `submitted`

---
<div style="page-break-after: always;"></div>

## <center> Cluster install: Bonus Material
## <center> <a name="scripted_install_lab"/>Auto-deployment

* If you are interested to learn about automating installs:
    * Fork/clone [Justin Hayes' auto-deploy project](https://github.com/justinhayes/cm_api/tree/master/python/examples/auto-deploy)
* No submissions are needed; you can research this repository as you wish.

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_cdh_key_points"/> Summary Points

* There is a depiction of Cloudera's [classic install paths] in the tools/ subdirectory.
* A complete CM HA configuration is [documented here](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/admin_cm_ha_overview.html)
* Remember that CDH operation does **not** depend on Cloudera Manager.
* CM has a REST API
    * Each API version is a superset of all prior versions
    * Try `http://<i>your_cm_host</i>:7180/api/version` in your browser
    * Some endpoints won't work for 4.x CDH deployments
        * CM API [is documented here](http://cloudera.github.io/cm_api/)
