# zabbix-web-apache-pgsql-zh

基于zabbix官方docker镜像，制作支持中文显示的zabbix web

官方镜像中，默认的中文配置是打开的，但是在界面上不能选择中文。

提示：You are not able to choose some of the languages, because locales for them are not installed on the web server.

用locale -a命令查看，系统里面没有中文字符集。

并且官方镜像中，zabbix-web使用的字体不支持，需要添加一个中文字体。

这个镜像修复了这些问题，但是启动之后界面还是英文，需要自己选择显示中文，因为选择显示什么语言是保存在数据库里面，不能在这个镜像中配置，只能是连接之后在界面上配置。

运行方式可参考官方文档

```shell
docker run --name zabbix-web-apache-pgsql \
-e DB_SERVER_HOST="psqlforzabbix" \
-e POSTGRES_USER="zabbix" \
-e POSTGRES_PASSWORD="tianyan" \
-e POSTGRES_DB="zabbix" \
--link psqlforzabbix:postgres \
--link zabbix-server-pgsql:zabbix-server \
-e PHP_TZ="Asia/Shanghai" \
-p 80:80 \
-d naturalsbq/zabbix-web-apache-pgsql-zh:centos-3.0-latest
```

