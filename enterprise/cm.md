<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---
<div style="page-break-after: always;"></div>

# <center> <a name="cm_monitor_customize_section"/>CM Monitoring & Customizing

* <a href="#cm_overview">CM's vocabulary</a>
* <a href="#cm_search_bar">CM search bar features</a>
* <a href="#cm_users_roles">CM users and roles</a>
* <a href="#cm_commands_history">Recent commands and history</a>
* <a href="#cm_monitors">Monitoring services and resources</a>
* <a href="#cm_alerts">Adding Alerts</a>
* <a href="#cm_health_checks">Health checks</a>
* <a href="#cm_charting_time_series">Charting time-series data</a>
* <a href="#cm_property_settings">Managing property settings</a>
* <a href="#cm_api_sampler">Sample CM API calls</a>

<!-- material to add
* Wizards include
    * Express Install
    * Add Service/Role
    * Upgrade CM and CDH
    * Enable HA (NameNode, Oozie, YARN RM)
* Some useful ones are buried here and there
    * <code><i>Service</i>->Instances->Add Role Instances->View By Host</code> (button)
-->

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_overview"/>CM Overview

<center> <img src="http://blog.cloudera.com/wp-content/uploads/2013/07/ClouderaManagerVocabulary.png" height="390" width="600"> </center>

---
<div style="page-break-after: always;"></div>

## <center> Cloudera Manager Server Implementation

* Written in Java
* Hooks & client APIs [are available](https://github.com/cloudera)
* Database preparation scripts: `/usr/share/cmf/schema`
* Command-line parameters: `/etc/default/cloudera-scm-server`

---
<div style="page-break-after: always;"></div>

## <center> Cloudera Manager Agent Implementation</center>

* Written in Python
* Configuration file: `/etc/cloudera-scm-agent/config.ini`
* Resources: `/usr/lib64/cmf/agent`
* Process control: `/var/run/cloudera-scm-agent`
    * Config files for CDH services are under `process/`
* Uses [supervisord](http://supervisord.org/) for process control

---
<div style="page-break-after: always;"></div>

## <center> Notes on Cloudera Manager vocabulary<p>

* [Philip Zeyliger's blog article on CM's design and operation](http://blog.cloudera.com/blog/2013/07/how-does-cloudera-manager-work/)  
* CM uses [service descriptors](http://cloudera.github.io/cm_api/docs/cm-concepts/) that evolve as new features emerge
    * [Primer for CM 4](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM4Ent/latest/Cloudera-Manager-Introduction/cmi_primer.html)
    * [Primer for CM 5](http://www.cloudera.com/documentation/enterprise/latest/topics/cm_intro_api.html)
* For deep-divers: compare the API for [4.7](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM4Ent/latest/Cloudera-Manager-Introduction/cmi_api.html) (v5), with [5.x](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Introduction/cm5i_api.html), (v6, v7)
* Example terms
    * Canary: a smoke test
    * Safety valve: window for additional service properties

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_search_bar"/> CM Search Bar Features

* Search bar in the upper right expands when selected
* The "/" hotkey forces whole-term match; otherwise partial-word
    * Try `/sq` vs. `sq`
* Searching a property name returns a config link
    * Try `dfs.datanode.max.xciever`
    * Then try `Transceiver`
* Use the Configuration tab for any service for a context-limited search
    * Go to the HDFS Configuration tab and type `locked`
* Notice each search result has a <i>type</i>

---
<div style="page-break-after: always;"></div>

## <center> Global search types

* CM types are also searchable
    * chart*
    * command
    * config*
    * global*
    * host
    * link*
    * role
    * service

Enter an object type in the search bar

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_users_roles"/>Users and roles

* Administration -> Users
    * Adding users recommended to differentiate admins
    * Supports role-based access limits
* CM 5.7 supports 11 roles
* `Administration -> Users -> Add Users` button
    * Select a role to see a description of its scope
    * Privileges per role are show in documentation

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_commands_history"/> Recent commands and history

* Home -> All Recent Commands
    * Up to 250 current/finished commands per display
    * Reports context (service), command status, start and finish times.
* Use the Audits tab to find past events
    * Available in home, service, role, and host instance pages
    * Time range filter from last 30m to last 30d (as of CM 5.1)
    * [Several other filters available](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_audits.html)
* Logs can also be downloaded

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_monitors"/>Monitoring services and resources</a>

* Type `monitor` in the Configuration tab search of any service
* [Eight general types ](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_monitoring_settings.html)
    * [Health for services, roles](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_service_monitoring.html)
    * [Resource management](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_resource_management_monitoring.html)
    * Directory free space
    * (MRv1) Activity
        * Includes job duration thresholds
    * YARN Applications
        * Visibility settings
    * Impala Queries
        * Memory cache thresholds
    * Alerts
    * Log Events

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_alerts">[Adding Alerts](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_monitoring_settings.html#concept_lmd_tss_1l_unique_1)</a>

* Administration -> Alerts
* Delivers to email or as SNMP traps
* May be associated with
    * Activity Monitor
    * Configuration changes (enable/disable only)
    * HBase (errors, poor region health)
    * Health metric thresholds (<font color="red">Bad</font> or <font color="orange">Concerning</font> result)
    * Log messages (regex matching)

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_health_checks"> [Health checks](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_health.html)</a>

* Cover services, roles, and hosts
* Two types
    * Pass-fail
    * ["Metric"](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM4Ent/4.7.1/Cloudera-Manager-Metrics/Cloudera-Manager-Metrics.html) - set to some numeric threshold
    * [Complete health tests list for CM5](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Health-Tests/Cloudera-Manager-Health-Tests.html#xd_583c10bfdbd326ba--43d5fd93-1410993f8c2--7ed7)
* Condition may be <font color="green">Good</font>, <font color="orange">Concerning</font>, or <font color="red">Bad</font>
    * Service results may be "rolled up" from subordinate tests (roles, instances)
        * A single Bad or Concerning result affects the whole
    * Some metric tests can also be <a href="#cm_charting_time_series">charted</a>

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_charting_time_series"> Charting metrics (time-series data) </a>

* CM 5's charts include a drop-down menu
* Charts are searchable by type or name
    * Try "canary duration"
* Chart builder and dashboard editor: CM -> Charts
    * [Documentation, CDH 5.1.1](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_chart_time_series_data.html)
    * A set of charts is called a [view](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM4Ent/4.7.1/Cloudera-Manager-Diagnostics-Guide/cmdg_views.html) in 4.x, a [dashboard](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_dashboards.html) in 5.x
* [Metric aggregations](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Diagnostics-Guide/cm5dg_metric_aggregation.html)
    * metric + timestamp pair + aggregating functions (min, max, avg, and stddev)
    * Sampling interval is determined by the monitor (Service or Host)
* Some 'cross-entity' aggregations provided
    * Cross-entity examples: all datanodes in the cluster, all datanodes in one rack
    * Aggregate examples: <code>fd_open_across_datanodes, total_fd_open_across_datanodes</code>

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_property_settings"> Managing property settings</a>

* [CDH properties by version](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Configuration-Properties/Cloudera-Manager-Configuration-Properties.html)
    * Organized by service
* [Host configuration properties](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Configuration-Properties/cm5config_host.html)
    * System services, directory free space, etc.
* [CM Server properties](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Configuration-Properties/cm5config_cmserver.html)
    * [Cloudera Management Service Properties](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Configuration-Properties/cm5config_mgmtservice.html)

---
<div style="page-break-after: always;"></div>

## <center> <a name="cm_api_sampler">Sample CM API calls</a>

* Version-based tours: cloudera.github.io/cm_api/apidocs/v[4567]/tutorial.html
    * Not a lot of variation from one to the next -- a good thing.
* [Examples using curl](http://cloudera.github.io/cm_api/docs/quick-start/)
* [Examples using Python](http://cloudera.github.io/cm_api/docs/python-client/)
* [Example using Java](http://cloudera.github.io/cm_api/docs/java-client/)
* Mark Brooks's script for [listing cluster service ports](https://github.com/onefoursix/cm-get-ports)
* Some often talked-about goals with the API
    * Fully automated, client-driven CM/CDH install
    * Dynamic multi-tenancy monitoring, utilization and tuning
    * The holy grail: [chargebacks](http://en.wikipedia.org/wiki/IT_chargeback_and_showback)

---
<div style="page-break-after: always;"></div>

## <center> Note on [Custom Service Descriptors](https://github.com/cloudera/cm_ext/wiki/CSD-Overview)

* Cloudera uses parcels to bundle CDH and other software
* We use CSDs to integrate software with Cloudera Manager's services
    * Monitoring and charting
    * Resource management (cgroups)
    * Service lifecycle controls
    * Property configuration
    * Host/role assignments
* A customer may ask about using CSDs
    * We do encourage adding third-party apps to HUE
    * But CM features are admin-driven, not user-driven
    * [One partner says they're useful](http://blog.cloudera.com/blog/2014/04/how-to-extend-cloudera-manager-with-custom-service-descriptors/) for supporting gateway/edge nodes

---
<div style="page-break-after: always;"></div>

## <center> CM Monitoring Lab

_Use CM to answer the following questions. For some questions, search will help you. Watch out for trick questions! (Some of these questions have been asked by customers.)  Put the questions and their answers in the file_ `enterprise/labs/0_CM_treasure_hunt.md`

* What is ubertask optimization?
* Where in CM is the Kerberos Security Realm value displayed?
* Which CDH service(s) host a property for enabling Kerberos authentication?
* How do you upgrade the CM agents?
* Give the `tsquery` statement used to chart Hue's CPU utilization?
* Name all the roles that make up the Hive service
* What steps must be compelted before integrating Cloudera Manager with Kerberos?

---
<div style="page-break-after: always;"></div>

## <center> CM Lab
## <center> Create a Custom Dashboard

* Create a new CM user `minotaur` in your cluster
* Assign the Configurator role  to `minotaur`
* Create a dashboard for `minotaur` and add any four charts  
* Put a screenshot of the new dashboard in the file `enterprise/labs/1_user_dashboard.png`

---
<div style="page-break-after: always;"></div>

## <center> CM Lab
## <center> Use the API to restart a service

* Browse or use `curl` on the endpoint `./api/v2/cm/deployment`
  * Store the output in `enterprise/labs/2_cluster_deployment.md`
* Follow the [tutorial for API v12](http://cloudera.github.io/cm_api/apidocs/v12/tutorial.html)
* Write `curl` statements that stop, start, and check the current state of your Hive service.
  * Add these statements and their output to `enterprise/labs/3_api_hive_state.md`
* Bonus: write a script `enterprise/labs/4_hive_restart.sh` to correctly restart Hive. The script should not try to start Hive until it has been stopped.
  * Or you can create the program in Python or Java. Name the file `enterprise/labs/5_hive_restart.[py|java]` as appropriate.

---
<div style="page-break-after: always;"></div>
