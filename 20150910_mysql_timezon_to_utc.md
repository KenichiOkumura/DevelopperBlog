https://blog.tagbangers.co.jp/ja/2015/09/10/MySQLのSystemTimeZoneをUTCにする

# MySQLのSystemTimeZoneをUTCにする

MySQLをBrewなどでインストールした場合、デフォルトのSystemTimeZoneはJSTになっています。
通常の開発では問題無いですが国際化とか考えるとUTCのが良いような。
そんな時の手順です。
​
## 1:my.cnfの設定を調べる
```
$ mysql --help | grep my.cnf
/etc/my.cnf /etc/mysql/my.cnf /usr/local/etc/my.cnf ~/.my.cnf
```
​
デフォだと↑な感じで左から読み込まれます。
今回は~/.my.cnfを作成する感じにします。
​
## 2:my.cnfに追記する
```
$ vi ~/.my.cnf
[mysqld_safe]
timezone = UTC
```
​
初めて編集する場合は真っ白けなので↑の2行だけ追記します。
​
## 3:MySQL再起動
```
$ mysql.server restart
Shutting down MySQL
. SUCCESS!
Starting MySQL
. SUCCESS!
```
​
## 4:ちゃんと変更されたかMySQLで確認
```
$ mysql
mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | UTC    |
| time_zone        | SYSTEM |
+------------------+--------+
```
​
こんなかんじでお手軽です。
元に戻す際は~/.my.cnfのファイルを削除してMySQLを再起動することで戻ります。
​
### 小ネタ
```
$ mysql
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```
​
こんなかんじのエラーが出てmysqlに繋がらない事があります。
こんな時はpsで起動中のmysqlを探してkillすると良いかもです。
```
$ ps aux | grep mysqld
sample 18491   0.0  2.8  3122552 464132   ??  S     9:18PM   0:09.36 /usr/local/Cellar/mysql/5.6.26/bin/mysqld --basedir=/usr/local/Cellar/mysql/5.6.26 --datadir=/usr/local/var/mysql --plugin-dir=/usr/local/Cellar/mysql/5.6.26/lib/plugin --bind-address=127.0.0.1
sample 18393   0.0  0.0  2461020   1120   ??  S     9:18PM   0:00.02 /bin/sh /usr/local/opt/mysql/bin/mysqld_safe --bind-address=127.0.0.1 --datadir=/usr/local/var/mysql
sample 26587   0.0  0.0  2423356    208 s016  R+   10:18AM   0:00.00 grep mysqld
$ kill -KILL 18491
```
​
HomebrewでMySQLをインストール時にLaunchAgentsにplistファイルを登録してると自動的に起動してくれると思います。