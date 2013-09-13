Hadoop (CDH 4.4) Ansible Playbook
=================================

This [Ansible](http://www.ansibleworks.com/) playbook will install a fully functional [Hadoop](http://hadoop.apache.org/)
and [HBase](http://hbase.apache.org/) cluster running Java 7 (supported by CDH 4.4), together
with [Ganglia](http://ganglia.sourceforge.net/), [Fluentd](http://fluentd.org/), [ElasticSearch](http://www.elasticsearch.org/)
and [Kibana3](http://three.kibana.org/) for monitoring and centralized log indexing.

Follow [@analytically](http://twitter.com/analytically) for updates.

## Requirements

  - Ansible 1.3+
  - Expects Ubuntu Server 13.04 (64 bit)
  - `ansibler` user in sudo group without password prompt (see Bootstrap section below)

### Cloudera ([CDH 4.4](http://www.cloudera.com/content/support/en/documentation/cdh4-documentation/cdh4-documentation-v4-latest.html)) Hadoop Roles

  - [`cdh_common`](roles/cdh_common/) - sets up Cloudera's Ubuntu repository and key
  - [`cdh_hadoop_common`](roles/cdh_hadoop_cmmon/) - common packages shared by all Hadoop/HBase nodes
  - [`cdh_hadoop_config`](roles/cdh_hadoop_config/) - common configuration shared by all Hadoop nodes
  - [`cdh_hbase_config`](roles/cdh_hbase_config/) - common configuration shared by all HBase nodes
  - [`cdh_hadoop_datanode`](roles/cdh_hadoop_datanode/) - installs Hadoop DataNode
  - [`cdh_hadoop_journal`](roles/cdh_hadoop_journal/) - installs Hadoop JournalNode
  - [`cdh_hadoop_namenode`](roles/cdh_hadoop_namenode/) - installs Hadoop NameNode
  - [`cdh_hadoop_zkfc`](roles/cdh_hadoop_zkfc/) - installs Hadoop Zookeeper Failover Controller
  - [`cdh_hbase_master`](roles/cdh_hbase_master/) - installs HBase-Master
  - [`cdh_hbase_regionserver`](roles/cdh_hbase_regionserver/) - installs HBase RegionServer
  - [`cdh_zookeeper_server`](roles/cdh_zookeeper_server/) - installs ZooKeeper Server

## Configure

Make sure you edit the following files:

- [`postfix_mandrill/defaults/main.yml`](postfix_mandrill/defaults/main.yml) and customize it for your [Mandrill](http://mandrill.com/) account

## Install Hadoop

To run Ansible:

```
site.sh
```

To e.g. just install ZooKeeper (available tags: ganglia, java, elasticsearch, kibana, rsyslog, tdagent, zookeeper, hadoop, hbase, configuration):

```
site.sh zookeeper
```

## Bootstrapping your machines

Paste your public SSH RSA key in `bootstrap/ansible_rsa.pub` and run `bootstrap.sh` to bootstrap the nodes
specified in `bootstrap/hosts`. See [`bootstrap/bootstrap.yml`](`bootstrap/bootstrap.yml`) for more information.

## Screenshots

![zookeeper](images/zookeeper.png)

![kibana](images/kibana.png)

### License

Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

Copyright 2013 [Mathias Bogaert](mailto:mathias.bogaert@gmail.com).