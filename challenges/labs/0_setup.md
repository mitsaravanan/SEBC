# Challenge Setup
The Amazon AWS region
```sh
Oregon (US West)
us-west-2.compute.amazonaws.com
```
AWS AMI information
```sh
Red Hat Enterprise Linux 7.2 (HVM), SSD Volume Type - ami-775e4f16
Red Hat Enterprise Linux version 7.2 (HVM), EBS General Purpose (SSD) Volume Type
```
Public IP that hosts MySQL
```sh
54.218.106.85
```
The command and output for ls /usr/java 
```sh
[root@ip-172-31-6-157 ec2-user]# ls /usr/java
ls: cannot access /usr/java: No such file or directory
```
Linux Users added
```sh
 useradd -u 2500 christie
 useradd -u 2501 weiner
 groupadd pictures
 groupadd bridges 
  usermod -a -G pictures weiner
 usermod -a -G bridges christie
```
/etc/passwd  output for users
```sh
christie:x:2500:2500::/home/christie:/bin/bash
weiner:x:2501:2501::/home/weiner:/bin/bash
```
/etc/group output for groups
```sh
pictures:x:2502:weiner
bridges:x:2503:christie
```