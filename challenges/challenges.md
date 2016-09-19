<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---
<div style="page-break-after: always;"></div>

# <center> Challenges - August 11, 2016 - Palo Alto, CA

* Overview
    * Build a CM-managed CDH cluster and secure it
* Place your work in the `challenges/labs` folder
    * Text output in Markdown (`.md`) files 
    * Screenshots in PNG format
* You can talk with each other and research online
    * But submit only your own work
* Push changes to your GitHub repo early and often -- don't wait until the end!
* If you break your cluster or your cluster breaks you:
    * Tell an instructor
    * Review the work you have pushed to GitHub
    * Create a new Issue and describe what happened

---
<div style="page-break-after: always;"></div>

## <center> Challenge Setup

* Create the Issue `Challenges Setup`
* Assign the Issue to yourself
* Add the requested information below to `challenges/labs/0_setup.md`:
    * Your OS release info source (e.g., `/etc/redhat-release`) and its contents
    * The command and output for `yum repolist enabled`
* The public FQDN of the node that will host your MySQL server
    * The command and output for `ls /etc/yum.repos.d` on this node
* Add the following Linux accounts to all nodes
    * User `gray` with a UID of `2500`
    * User `baumgarner` with a UID of `2501`
    * Create the group `giants` and add `baumgarner` to it
    * Create the group `athletics` and add `gray` to it
* List the `/etc/passwd` entries for `gray` and `baumgarner` in your setup file
* List the `/etc/group` entries for `giants` and `athletics` in your setup file
* Push this work to your GitHub repo 
* Assign the Issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 1: Install a MySQL server

* Create the Issue `Install MySQL`
* Assign the Issue to yourself
* Use the file `challenges/labs/1_mysql.md` for information requested below:
* Install a MySQL 5.6.x server using a YUM repository
    * Use the same node you specified in the Setup 
    * Capture (again) the output of `yum repolist enabled`
* Install on all nodes in your cluster:
    * The MySQL client package (and any dependencies)
    * The MySQL JDBC connector 
* Create the following databases and write the appropriate grants
    * For Cloudera Manager: `scm` 
    * For the Reports Manager: `rman`
    * For Hive Metastore: `hive` 
    * For Oozie: `oozie`
    * For Hue: `hue` 
* Also add the following 
    * The command and output for `mysql --version`
    * The list of databases as reported by MySQL
    * The grants for the `scm` database
* Push this work to your GitHub repo
* Assign the issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 2: Install Cloudera Manager

* Create the Issue `Install CM`
* Assign the Issue to yourself
* Use the file `challenges/labs/2_cm.md` for the output required below
* List the node that will host Cloudera Manager
    * It cannot be the same node as the MySQL server
* Configure a Cloudera Manager package repository for the 5.7.0 release
    * List the repo file and show its contents 
* Configure Cloudera Manager 
    * Show the contents the the `db.properties` file
* Complete and list the following statements in your file:
    * The permanent generation space allocated to the CM server is _________.
    * The CM file `db.properties` is created by _________.
* Push this work to your GitHub repo
* Assign the issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 3 - Install CDH

* Create the Issue `Install CDH`
* Assign the issue to yourself
* Install the latest version of CDH 5.5.x
* Install the Coreset only -- nothing extra
* Name your cluster using your GitHub handle
* Use the file `challenges/labs/3_cm.md` for the output required below
* Create user directories in HDFS for `gray` and `baumgarner`
* Submit the following:
    * Command and output for `hdfs dfs -ls /user`
    * Command and output for `hadoop classpath`
    * Command and output for the CM API call that lists the cluster's full deployment
* Login to the HUE console; install the Hive sample data
    * Capture your Hue home page and save as `challenges/labs/3_hue_installed.png`
* Push this work to your GitHub repo
* Assign the issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 4 - HDFS Testing

* Create the Issue `HDFS Tested`
* Assign the issue to yourself
* As user `gray`, use `teragen` to generate a 51,200,000-record file
    * Set the block size to 48 MB
    * Use the `time` command to capture job duration
    * Use the output directory `tgen48`
* List the following in `challenges/labs/4_teragen.md`
    * The `teragen` command you used 
    * How long the job took to run
    * The command and output of `hdfs dfs -ls /user/gray/tgen48`
    * How many blocks were created to store this file
* Push this work to your GitHub repo
* Assign the issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 5 - Kerberize the cluster

* Create the Issue `Kerberize cluster`
* Assign the issue to yourself
* Put a Kerberos server on the node hosting Cloudera Manager
    * Your realm will be your GitHub handle in uppercase, followed by `.UK`
    * Example: `MFERNEST.UK`
* Create Kerberos principals for `gray` and `baumgarner`
* Integrate Cloudera Manager with the Kerberos server
* Run the `terasort` program as `gray` using `/user/gray/tgen48`
    * Store the command and job output in `challenges/labs/5_terasort.md`
* Run the Hadoop `pi` program as the user `baumgarner`
    * Add the command and output to `challenges/labs/5_pi.md`
* Submit:
    * The `kinit` and `klist` commands and output in `challenges/labs/5_kinit.md`
    * A list of all Kerberos principals in `challenges/labs/5_principals.md`
    * All the configuration files in `/var/kerberos/krb5kdc/' with the following changes:
        * Prepend a `5_` and add `.md` to each file name.
        * Example: `5_kdc.conf.md`
* Push this work to your GitHub repo
* Assign the issue to your instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 6 - Configure Sentry

* Create the Issue `Configure Sentry`
* Install and configure Sentry
* Make `baumgarner` a Sentry administrator
* Login to `beeline` 
    * Create an `designated` role that has rights to the `default` database
        * Map the `athletics` group to this role
    * Create an `pitcher` role that has `SELECT` privileges on all tables in `default
        * Map the `giants` group to this role
* Login to `beeline` as the principal for `gray`
    * List the result of `SHOW TABLES;` in `challenges/labs/6_results.md`
* Login to `beeline` as the principal for `baumgarner`
    * List the result of `SHOW TABLES;` in the same file
* Push all work to your GitHub repo

---
<div style="page-break-after: always;"></div>

## <center> If you finish, or once time is called:

* Make one last push to your GitHb repo, if necessary
* Complete [this quick survey](https://docs.google.com/forms/d/1cFfvTHKz8TEYZgkkZSQFAYtULxsuc-S1qE2kiDFSrBo/viewform)
* Add your course feedback `challenges/labs/7_feedback_final.md`. Remember, your challenges are considered
unfinished without this content.
* Please include the following:
    * Describe the boot camp in your own words: was it camp useful, too difficult, too simple? 
    * Which topic was least familiar to you? Which topic was most familiar?
    * Which topic did you feel was most instructive? Which topic was least helpful to you?
    * How long do you think you'll need to be ready to install a production cluster by yourself? What more do you need to work on?
* It has been a pleasure working with you this week! Safe travels home.
    * `mfernest@cloudera.com`

---
<div style="page-break-after: always;"></div>
