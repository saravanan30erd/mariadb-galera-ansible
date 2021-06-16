### Deploy the Galera Cluster.

A Multi-Master Cluster of MariaDB based on synchronous replication.

## Description
[Galera Cluster](https://galeracluster.com/) is a synchronous multi-master replication plug-in for InnoDB. It is very different from the regular MySQL Replication, and addresses a number of issues including write conflicts when writing on multiple masters, replication lag and slaves being out of sync with the master. Users do not have to know which server they can write to (the master) and which servers they can read from (the slaves).

## Getting Started
```shell
ansible-playbook -i inventories/galera/test-db/hosts galera.yml -e 'first_time=true'
```

## Variables
Variable | Default | Description
--- | --- | ---
[`ip`](inventories/galera/test-db/hosts.ini#L1) | - | private IP of the VM
[`dns_domain`](inventories/galera/test-db/group_vars/all.yml#L2) | - | specify the hostname of the node VM
[`mariadb_version`](inventories/galera/test-db/group_vars/all.yml#L5) | - | specify the [version of MariaDB](https://mariadb.com/kb/en/mariadb-server/#:~:text=MariaDB%20Server%2010.5,supported%20until%2024%20June%202025.) to be installed.
[`galera_cluster_name`](inventories/galera/test-db/group_vars/all.yml#L7) | 10.5 | specify [wsrep_cluster_name](https://mariadb.com/kb/en/galera-cluster-system-variables/#wsrep_cluster_name).
[`first_time`](inventories/galera/test-db/group_vars/all.yml#L10) | false | is the custom environment variable defined to determine if its first run to setup the cluster.
[`mysql_root_password`](inventories/galera/test-db/group_vars/all.yml#L13) | - | specify mariadb root password.
[`innodb_buffer_pool_size`](inventories/galera/test-db/group_vars/all.yml#L16) | 3096M | set [innodb_buffer_pool_size](https://mariadb.com/kb/en/innodb-buffer-pool/#innodb_buffer_pool_size) for MariaDB.
[`mariadb_repo_url`](inventories/galera/test-db/group_vars/all.yml#L19) | [default_link](http://yum.mariadb.org/10.5/centos7-amd64) | It is [repository_url](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-setting_repository_options), a URL to the directory where the repodata directory of a MariaDB repository is located.

### Tested Versions
* CentOS Linux release 7.9.2009 (Core)
* Ansible 2.11.1
* [MariaDB 10.5.10](https://mariadb.com/kb/en/mariadb-10510-release-notes/)
* [Galera 4](https://mariadb.com/kb/en/meta/galera-versions/)