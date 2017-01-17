---
layout: post
title: Integrate MongoDB with ElasticSearch
date: 2017-01-16 12:04:12
categories: 
---

## Table of Contents

* [Setup MongoDB](#setup-mongodb)
  * [Install MongoDB](#install-mongodb)
  * [Default Path of DB and Config file](#default-path-of-db-and-config-file)
  * [Change Default Setting](#change-default-setting)
  * [Check Service](#check-service)
* [Setup ElasticSearch](#setup-elasticsearch)
  * [Install ElasticSearch](#install-elasticsearch)
  * [Check Service](#check-service)
* [Integrate MongoDB with ElasticSearch](#integrate-mongodb-with-elasticsearch)
  * [Configure MongoDB Replica](#configure-mongodb-replica)
  * [Install ElasticSearch Plugins](#install-elasticsearch-plugins)
* [Test Case](#test-case)
  * [Configure River](#configure-river)
  * [Feed Data to MongoDB](#feed-data-to-mongodb)
  * [Query Check](#query-check)

## Setup MongoDB

### Install MongoDB

```bash
# install mongodb 3.0
brew install homebrew/versions/mongodb30
# create link if not linked
brew link mongodb30
# create db dir
mkdir -p /data/db
# add permission
sudo chmod 777 /data/db
```

### Default Path of DB and Config file

With homebrew, the default path for db and config might be different. To check the default path:

```bash
# check path of default config file
ps -xa | grep mongod  # => /usr/local/etc/mongod.conf
# check path of default db
vim /usr/local/etc/mongod.conf  # => /usr/local/var/mongodb
```

A copy of default config file:

```
systemLog:
  destination: file
  path: /usr/local/var/log/mongodb/mongo.log
  logAppend: true
storage:
  dbPath: /usr/local/var/mongodb
net:
  bindIp: 127.0.0.1
```

### Change Default Setting

Change config `dbPath` and `engine` in `/usr/local/etc/mongod.conf`:

```bash
systemLog:
  destination: file
  path: /usr/local/var/log/mongodb/mongo.log
  logAppend: true
storage:
  dbPath: /data/db
  engine: mmapv1
net:
  bindIp: 127.0.0.1
```

Reset config and service

```bash
brew services restart mongodb30 
```

### Check Service

Start service with:

```
mongod
```

## Setup ElasticSearch

### Install ElasticSearch

```bash
# install elasticsearch 1.7
brew install elasticsearch@1.7
# create link if not linked
brew link elasticsearch@1.7
# start service
brew services start elasticsearch@1.7
```

### Check Service

```
# check if it's running
curl -XGET http://localhost:9200
```

## Integrate MongoDB with ElasticSearch

### Configure MongoDB Replica

Setup replica set, in order to create a data tunnel between MongoDB and ElasticSearch.

Before configuring replica, make sure all mongo services are down

```
# kill all services listed
ps aux | grep mongod
```

Start configuring

```
# in one terminal window
mongod --replSet "rs0"
```

```
# in another terminal window
mongo
# initiate replica
> rs.initiate()
# verify replica config
> rs.config()
> rs.status()
```

### Install ElasticSearch Plugins

**Mapper Attachments Plugin**

```
cd /usr/local/Cellar/elasticsearch@1.7/1.7.6
# es-1.7 is compatiable with 2.7.1
bin/plugin install elasticsearch/elasticsearch-mapper-attachments/2.7.1
```

**MongoDB River Plugin**

```
cd /usr/local/Cellar/elasticsearch@1.7/1.7.6
bin/plugin --install com.github.richardwilly98.elasticsearch/elasticsearch-river-mongodb/2.0.9
```

**Mobz Plugin**

Enable access to ES through web interface

```
bin/plugin -install mobz/elasticsearch-head
```

Now we could access to ES through

```
http://localhost:9200/_plugin/head/
```

## Test Case

### Configure River

```
curl -XDELETE localhost:9200/_river
```

```
curl -XPUT 'http://localhost:9200/_river/mongodb/_meta' -d '{ 
  "type": "mongodb", 
  "mongodb": { 
    "db": "testmongo", 
    "collection": "person"
  }, 
  "index": {
    "name": "mongoindex", 
    "type": "person" 
  }
}'
```

### Feed Data to MongoDB

```
mongo 
> use testmongo
> var p = {firstName: "Chen", lastName: "Huang"}
> db.person.save(p)
```

### Query Check

```
curl -XGET 'http://localhost:9200/mongoindex/_search?q=firstName:Chen'
```
