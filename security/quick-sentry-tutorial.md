## <center> A Quick Sentry Tutorial </center>

* This tutorial assumes:
  * Your cluster has been Kerberized
  * You've reviewed the [Hive SQL syntax for Sentry](https://www.cloudera.com/documentation/enterprise/latest/topics/sg_hive_sql.html)

### Create test accounts
* Create a new Linux account for administering Sentry
* Also create a Kerberos principal for this user

### Configure Sentry to recognize the account as an administrator
* Add the user to the `sentry.service.admin.group` list in CM
* Restart Sentry, HUE, Hive, and Impala services

### Verify user privileges
* Authenticate the user as a Kerberos principal using `kinit`
* Use `beeline` to show the user can't see any tables
    * `!connect jdbc:hive2://localhost:10000/default;principal=hive/hs2.node.com@REALM.COM`
    * When prompted to login, use your Linux account name and password.
    * At the `beeline` prompt, enter `SHOW TABLES;`
    * The command returns an empty set to show access was not authorized.

### Create a Sentry role with full privileges
* Enter the following statements through `beeline`
    * `CREATE ROLE sentry_admin;`
    * `GRANT ALL ON SERVER server1 TO ROLE sentry_admin;`
    * `GRANT ROLE sentry_admin TO GROUP {user_primary_group};`
    * `SHOW TABLES;`
* The statement should return all tables available under `server1`

### Create some test users
* Create other users & groups on all cluster nodes
    * `$ sudo groupadd selector`
    * `$ sudo groupadd inserters`
    * `$ sudo useradd -u 1100 -g selector george`
    * `$ sudo useradd -u 1200 -g inserters ferdinand`
    * `$ kadmin.local: add_principal george`
    * `$ kadmin.local: add_principal ferdinand`

### Create some test roles
* Login to `beeline` as your admin user
    * `CREATE ROLE read_auth;`
    * `CREATE ROLE write_auth;`

### Grant read privilege for all tables to `read_auth`
* `GRANT SELECT ON DATABASE default TO ROLE read_auth;`
* `GRANT ROLE read_auth TO GROUP selector;`

### Grant read privilege for `default.sample07` only to 'write_auth':
* `REVOKE ALL ON DATABASE default FROM ROLE write_auth;`
* `GRANT SELECT ON default.sample_07 TO ROLE write_auth;`
* `GRANT ROLE write_auth TO GROUP inserters;`

### `kinit` as george and login to beeline
* `SHOW TABLES;`
* `george` should be able to see all tables
* Authenticate as `ferdinand`
    * `ferdinand` should see `sample_07` only
