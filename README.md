# GrayLog
Centralized logging using Graylog

# Scenario
Consider your environment has a number of servers. Whenever there is an issue being reported, you have to manually log into each server and check logs to troubleshoot it. Searching for a particular error across hundreds of log files on hundreds of servers becomes a pain if the environment grows bigger. Moreover, there is no way to alert if there is any occurrence of error / abnormal activity in the log files unless the issue is being reported by the application team or after the service becomes unavailable.

# Solution:
A common approach to this problem is to setup a centralized logging solution so that multiple logs can be aggregated in a central location. The advantage is not just about centralizing these logs, but getting a better insight of what each system is doing at any point in time. We can parse custom logs using grok pattern or regex and create fields. Segregating the logs using fields helps to slice and dice the log data which helps in doing various analysis. Centralized logging plays a major role as part of operations troubleshooting and analysis.

#### There are many famous open source / enterprise products for centralized logging such as,
  - Elk
  - Splunk
  - GrayLog

`` One other major player of centralized logging is ELK which is again an open source like graylog. Graylog has some edge over ELK in some aspects when considering out of the box features. To name a few ``
  - Graylog provides User management out of the box Has an inbuilt alert system
  - Graylog is able to accept and parse RFC 5424 and RFC 3164 compliant syslog messages out of the box
  - Messages forwarded by rsyslog or syslog-ng are usually parsed flawlessly
 
See [GrayLogInstall Centos.md](https://github.com/harishchanderdalal/graylog/blob/master/grayloginstallation.md)

### Installation
 - Java
 - Mongo
 - Elasticsearch
 - Graylog

## Java
```
$ sudo yum install java-1.8.0-openjdk-headless.x86_64
```

## Mongo Db - NoSql DB
Create a repository file to get the latest version :-
```
$ /etc/yum.repos.d/mongodb-org.repo
```
Add the below content to above file :-
```
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
```
Install and start the service
```
$sudo yum install mongodb-org
$ sudo systemctl daemon-reload
$ sudo systemctl enable mongod.service
$ sudo systemctl start mongod.service
$ sudo systemctl --type=service --state=active | grep mongod
```
## ElasticSearch
Create GPG key :-
```
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```
Create a repository file to get the latest version :-
```
$ /etc/yum.repos.d/elasticsearch.repo
```
Add the below content to above file :-
```
[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/oss-6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
Update the cluster name in ElasticSearch:-
```
vim /etc/elasticsearch/elasticsearch.yml
```
set the cluster name:- 
```
cluster.name: YOURNAME
```
Install and start the service :-
```
$ sudo yum install elasticsearch-oss
$ sudo systemctl daemon-reload
$ sudo systemctl enable elasticsearch.service
$ sudo systemctl restart elasticsearch.service
$ sudo systemctl --type=service --state=active | grep elasticsearch
```

## GrayLog
Install Graylog Repo:-
```
sudo rpm -Uvh https://packages.graylog2.org/repo/packages/graylog-3.3-repository_latest.rpm
```
Install Graylog Server:-
```
sudo yum install graylog-server
```
Create password_secret:- 
See [Url Genrate Password](https://8-p.info/pwgen/?)
- Password must be 16 CHAR
- No Capital Word

Create root_password_sha2:-
```
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```
Update both paassword in 
```
vim /etc/graylog/server/server.conf
```
Install and start the service :-
```
$ sudo systemctl daemon-reload
$ sudo systemctl enable graylog-server.service
$ sudo systemctl start graylog-server.service
$ sudo systemctl --type=service --state=active | grep graylog
```
