# Install MySQL on CentOS
You can install MySQL on CentOS by the following steps.

## Add Yum repository
`$ sudo rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el6-7.noarch.rpm`

## Confirm install packages
`$ sudo yum info mysql-community-server`

## Install MySQL
`$ sudo yum install mysql-community-server`

## Confirm MySQL version
`$ mysql --version`

## Edit settings file
`vi /etc/my.cnf`

```
[mysqld]
character-set-server=utf8mb4
[client]
default-character-set=utf8mb4
```

## Start MySQL
`service mysqld start`

## Confirm initial password
`grep 'temporary password' /var/log/mysqld.log`

## Security settings
`mysql_secure_installation`
