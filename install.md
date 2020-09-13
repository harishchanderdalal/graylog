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
Install and start the service :-
```
$ sudo yum install elasticsearch-oss
$ sudo systemctl daemon-reload
$ sudo systemctl enable elasticsearch.service
$ sudo systemctl restart elasticsearch.service
$ sudo systemctl --type=service --state=active | grep elasticsearch
```
