https://blog.tagbangers.co.jp/ja/2017/03/14/docker_mysql_latin1_utf-8

# Dockerでmysqlを建てた際に文字コードをよしなにする
連投です。奥村です。
最近弊社ではdocker推しなのでビッグウェーブに乗る意味も兼ねて小ネタを。

dockerでmysqlを立てる場合の超簡易なコマンドは下記の通り。

`$ docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql`
上のコマンドで立ち上げたmysqlでデータベースを作成して文字コード確認してみると下記の通り。

```
~ $ docker exec -it mysql bash
root@501cbebbcdf3:/# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 5.7.17 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show variables like "chara%";
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | latin1                     |
| character_set_connection | latin1                     |
| character_set_database   | latin1                     |
| character_set_filesystem | binary                     |
| character_set_results    | latin1                     |
| character_set_server     | latin1                     |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.01 sec)
```

ありがちなlatin1さん
よくある対処法としてはmy.cnfをいじってしまう対応だけどDockerだからいまいち…。
そんなときはコンテナ立ち上げ時にオプション値指定してあげるだけで解決します。
`[--character-set-server=utf8 --collation-server=utf8_unicode_ci]` を追加して実行してみます。

```
~ $ docker run -d --name blog -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql --character-set-server=utf8 --collation-server=utf8_unicode_ci
7851f576e101a87791154a3f71120c132fa3a1e06ec608575614e17a318a3644
~ $ docker exec -it blog bash
root@7851f576e101:/# mysql -uroot -p
Enter password:
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
root@7851f576e101:/# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.17 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show variables like "chara%";
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | latin1                     |
| character_set_connection | latin1                     |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | latin1                     |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.00 sec)
```

Good by latin1!