### Deploy the Galera Cluster.

A Multi-Master Cluster of MariaDB based on synchronous replication.

## Description
[Galera Cluster](https://galeracluster.com/) is a synchronous multi-master replication plug-in for InnoDB. It is very different from the regular MySQL Replication, and addresses a number of issues including write conflicts when writing on multiple masters, replication lag and slaves being out of sync with the master. Users do not have to know which server they can write to (the master) and which servers they can read from (the slaves).

## Getting Started
```shell
ansible-playbook -i inventories/galera/test-db/hosts galera.yml -e 'first_time=true'
```

### Variables
* [ip=10.0.0.45](inventories/galera/test-db/hosts.ini#L1) mentioned in the ansible inventory is set to private IP because when using public cloud services you may use [ansible_host](inventories/galera/test-db/hosts.ini#L1) to configure with public IP.
* [dns_domain](inventories/galera/test-db/group_vars/all.yml#L2) specify the hostname of the node VM
* [mariadb_version](inventories/galera/test-db/group_vars/all.yml#L5) specify the [version of MariaDB](https://mariadb.com/kb/en/mariadb-server/#:~:text=MariaDB%20Server%2010.5,supported%20until%2024%20June%202025.) to be installed.
* [galera_cluster_name](inventories/galera/test-db/group_vars/all.yml#L7) specify [wsrep_cluster_name](https://mariadb.com/kb/en/galera-cluster-system-variables/#wsrep_cluster_name).
* [first_name](inventories/galera/test-db/group_vars/all.yml#L10) is the custom environment variable defined to determine if its first run to setup the cluster.
* [mysql_root_password](inventories/galera/test-db/group_vars/all.yml#L13) specify mariadb root password.
* [innodb_buffer_pool_size](inventories/galera/test-db/group_vars/all.yml#L16) set [innodb_buffer_pool_size](https://mariadb.com/kb/en/innodb-buffer-pool/#innodb_buffer_pool_size) for MariaDB.
* [mariadb_repo_url](inventories/galera/test-db/group_vars/all.yml#L19) is [repository_url](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-setting_repository_options), a URL to the directory where the repodata directory of a MariaDB repository is located.

### Tested Versions
* CentOS Linux release 7.9.2009 (Core)
* Ansible 2.11.1
* [MariaDB 10.5.10](https://mariadb.com/kb/en/mariadb-10510-release-notes/)
* [Galera 4](https://mariadb.com/kb/en/meta/galera-versions/)