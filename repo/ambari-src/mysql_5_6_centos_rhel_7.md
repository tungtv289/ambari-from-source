Config mysql 5.6 Repo

```
yum install wget

wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm

rpm -ivh mysql-community-release-el7-5.noarch.rpm

ls -1 /etc/yum.repos.d/mysql-community* #validate package
```

Install Mysql

```
systemctl start mysqld
```

Set password

```
mysql_secure_installation
```

Login mysql

```
mysql -uroot -p123456
```

New User and Grant Permissions in MySQL

```
mysql> CREATE DATABASE ambari;

mysql> CREATE USER 'ambari'@'%' IDENTIFIED BY 'bigdata';

mysql> GRANT ALL PRIVILEGES ON ambari.* TO 'ambari'@'%' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;

mysql> use ambari;

mysql> source /var/lib/ambari-server/resources/Ambari-DDL-MySQL-CREATE.sql;

```