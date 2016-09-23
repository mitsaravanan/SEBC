<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---
<div style="page-break-after: always;"></div>

# <center> Challenges - September 23, 2016 - New York City, NY

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
* Assign the Issue to yourself and label it `started`
* Add the requested information below to `challenges/labs/0_setup.md`:
    * The AWS region you're using for your nodes
    * The AMI you're using for your nodes
* The public IP of the node you will use to host your MySQL server
    * The command and output for `ls /usr/java` on this node
* Add the following Linux accounts to all nodes
    * User `christie` with a UID of `2500`
    * User `weiner` with a UID of `2501`
    * Create the group `pictures` and add `weiner` to it
    * Create the group `bridges` and add `christie` to it
* List the `/etc/passwd` entries for `christie` and `weiner` in your setup file
* List the `/etc/group` entries for `pictures` and `bridges` in your setup file
* Push this work to your GitHub repo
* Add the label `finished` (or `submitted`) to your Issue
* If you're sitting closest to the left wall, assign the Issue to `mridley`.
* If you're sitting closest to the right wall, assign the Issue to `mfernest`.

---
<div style="page-break-after: always;"></div>

## <center> Challenge 1: Install a MySQL server

* Create the Issue `Install MySQL`
* Assign the Issue to yourself and label it `started`
* Install MySQL 5.5.x server using the YUM repository from `dev.mysql.com`
    * Use the node you specified in the Setup exercise
    * Copy `/etc/yum.repos.d/mysql-community.repo` to `challenges/labs/mysql-community.repo.md`
* On all cluster nodes:
    * Install the MySQL client package
    * Copy the MySQL JDBC connector to the appropriate directory
* Start the `mysqld` service
* Create the following databases, but do not grant permissions for them yet
    * `scm`
    * `rman`
    * `hive`
    * `oozie`
    * `hue`
    * `sentry`
* Add the following to `challenges/labs/1_mysql.md`
    * The command and output of `mysql --version`
    * The command and output for a list of databases in MySQL
    * The command and output for a list of grants in MySQL
* Push this work to your GitHub repo
* Add the label 'finished` to the Issue
* Assign the issue to the same instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 2: Install Cloudera Manager

* Create the Issue `Install CM`
* Assign the Issue to yourself and label it `started`
* Use a different node to install Cloudera Manager
* Configure the CM repo to install the `5.8.0` release
    * List the command and contents of `/etc/yum/repos.d` in `challenges/labs/2_cm.d`
    * Copy the `cloudera-manager.repo` file to `challenges/labs/2_cloudera-manager.repo.md`
* Configure Cloudera Manager
    * Copy the `db.properties` file to `challenges/labs/2_db.properties.md`
    * Grant permission for CM to access MySQL _only_ from the CM node
    * Copy the `GRANT` statement you use to `challenges/labs/2_cm.d`
* Start the Cloudera Manager server
    * Copy `head -1 /var/log/cloudera-scm-server/cloudera-scm-server.log` and its output to `challenges/labs/2_cm.d`
    * Copy `grep "Started Jetty server" /var/log/cloudera-scm-server/cloudera-scm-server.log` and its output to the same file
* Push this work to your GitHub repo and add the label 'finished` to the Issue
* Assign the issue to the same instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 3 - Install CDH

* Create the Issue `Install CDH`
* Assign the issue to yourself and label it `started`
* Install the CDH 5.7.x; deploy the Coreset services only
* When the screen for testing database connections appears, issue the `GRANT` statements you'll need
    * Use `FLUSH PRIVILEGES;` to ensure they're loaded for testing
* Create the file `challenges/labs/3_cm.md`
    * Copy `SHOW GRANTS FOR <database>` and the output for `rman`, `hive`, and `oozie` into the file
* Create user directories in HDFS for `christie` and `weiner`
* Add the following to the file:
    * Command and output for `hdfs dfs -ls /user`
    * Command and output for `hadoop classpath`
    * The first item output from the CM API call `../api/v13/hosts` using your browser
* Login to the Hue console; install the Hive sample data
    * Get a screenshot of the Hue home page and save as `challenges/labs/3_hue_installed.png`
* Push this work to your GitHub repo and label the Issue `finished`
* Assign the issue to the same instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 4 - HDFS Testing

* Create the Issue `HDFS Tested`
* Assign the issue to yourself and label it `started`
* As user `christie`, use `teragen` to generate a 51,200,000-record file
    * Set the block size to 64 MB
    * Use the `time` command to capture job duration
    * Name the target directory `tgen64`
* Put the following in a file named `challenges/labs/4_teragen.md`
    * The full `teragen` command line you use
    * The output of the `time` command
    * The command and output of `hdfs dfs -ls /user/christie/tgen64`
    * Indicate many blocks were created to hold this file's data
* Push this work to your GitHub repo and label the Issue `finished`
* Assign the issue to the same instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 5 - Kerberize the cluster

* Create the Issue `Kerberize cluster`
* Assign the issue to yourself and label it `started`
* Install a Kerberos server on the same node as MySQL
    * Your realm will be your GitHub handle in uppercase, followed by `.NYC`
    * Example: `MFERNEST.NYC`
* Create Kerberos principals for `christie` and `weiner` as well as `cloudera-scm`
* Use Cloudera Manager to integrate Kerberos with the cluster
* Run the `terasort` program as `christie` using `/user/christie/tgen64`
    * Store the command and job output in `challenges/labs/5_terasort.md`
* Run the Hadoop `pi` program as the user `weiner`
    * Add the command and output to `challenges/labs/5_pi.md`
* Also submit:
    * All the `kinit` and `klist` commands and output you used in `challenges/labs/5_kinit.md`
    * A list of all principals in `challenges/labs/5_principals.md`
    * The configuration files in `/var/kerberos/krb5kdc/' with these changes:
        * Prepend a `5_` and add `.md` to each file name
        * Example: `5_kdc.conf.md`
* Push this work to your GitHub repo and label the Issue `finished`
* Assign the issue to the same instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 6 - Configure Sentry

* Create the Issue `Configure Sentry`
* Install and configure Sentry
* Make `weiner` a Sentry administrator
* Login to `beeline`
    * Create an `governor` role that has rights to the `default` database
        * Map the `bridges` group to this role
    * Create a `lawmaker` role that has `SELECT` privileges on all tables in `default`
        * Map the `pictures` group to this role
* Login to `beeline` as the principal for `christie`
    * List the result of `SHOW TABLES;` in `challenges/labs/6_results.md`
* Login to `beeline` as the principal for `weiner`
    * List the result of `SHOW TABLES;` in the same file
* Push all work to your GitHub repo

---
<div style="page-break-after: always;"></div>

## <center> Once you finish, or when time is called:

* Commit any remaining changes in your repo and push them to GitHub
* Complete [this quick survey](https://docs.google.com/forms/d/e/1FAIpQLSfBUSFtEcVFzv_9bHwh9dG8ZHzmQk6wWNLFZAVUtdMd1sgZ6g/viewform)
* Write course feedback in `challenges/labs/7_feedback_final.md`.
Your challenges are not evaluated unless these questions are answered:
    * Describe the boot camp: was it useful, difficult, simple?
    * Which topic was least familiar to you? Which topic was most familiar?
    * Which topic did you feel was most helpful? Which topic was not useful, if any?
    * How long before you are ready to to install a production cluster by yourself? What do you need to work on?
* It has been a pleasure working with you this week! We hope your travel home is safe and comfortable.
    * `mfernest@cloudera.com`
    * `mridley@cloudera.com`

---
<div style="page-break-after: always;"></div>
