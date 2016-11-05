## MySQL

### Install MySQL5.7 on Ubuntu 16.04 LTS

when use apt-get repo to install, if you are not reply a password for root account in the process, then while install complete, you must use `sudo mysql -u root` to get into mysql. The solution is remove mysql totally.

### Remove mysql totally

```shell
## 1. remove apt deb package
sudo apt-get autoremove --purge mysql-server

## 2. remove the configure files
sudo rm -rf /etc/mysql

## 3. remove the lib files.(!important)
sudo rm -rf /var/lib/mysql
```

## Configure files

```
ServiceController/servicedaemon/src/main/resources/config.properties
auroraWS/lib/zero_mq.rb: broker_address
```

## Question

* Rails server, see [Using zeromq out put failed due to ‘zmq_ctx_new’ nout found]

```shell
## `/usr/local/bundle/gems/ffi-1.9.13/lib/ffi/library.rb:275:in `attach_function': Function 'zmq_ctx_new' not found in [libzmq.so] (FFI::NotFoundError)`
sudo apt-get install libzmq3-dev
```
- MySQL connect, see [installing-mysql-in-docker-fails-with-error-message-cant-connect-to-local-mysq]

```shell
## `ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)`
mysql -h localhost -P 3306 --protocol=tcp ## --protocol
```
- 错误 101 (net::ERR_CONNECTION_RESET)：连接已重置

```shell
ping host ## May caused by cache, ping the host to solve it.
```

- Mysql2::Error: Table 'performance_schema.session_variables' doesn't exist: SHOW VARIABLES LIKE 'character_set_database'

```shell
# The MySQL may be damaged, your can reinstall and upgrade it to fix the system data.
sudo mysql_upgrade -u root -p
sudo service mysql restart
```

- panic: standard_init_linux.go:175: exec user process caused "exec format error" [recovered]
```shell
# Add #!/bin/bash into bash script file.
```
See more at [Will Anderson].

[Using zeromq out put failed due to ‘zmq_ctx_new’ nout found]: https://github.com/logstash-plugins/logstash-output-zeromq/issues/17
[installing-mysql-in-docker-fails-with-error-message-cant-connect-to-local-mysq]: (http://stackoverflow.com/questions/23234379/installing-mysql-in-docker-fails-with-error-message-cant-connect-to-local-mysq)

[Will Anderson]: http://willi.am/blog/2016/08/11/docker-for-windows-dealing-with-windows-line-endings/
