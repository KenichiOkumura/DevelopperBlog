# MySQLのSystemTimeZoneをUTCにする

<p>MySQLをBrewなどでインストールした場合、デフォルトのSystemTimeZoneはJSTになっています。
	<br>通常の開発では問題無いですが国際化とか考えるとUTCのが良いような。
	<br>そんな時の手順です。</p>
​
<h2>1:my.cnfの設定を調べる</h2><pre>$ mysql --help | grep my.cnf
/etc/my.cnf /etc/mysql/my.cnf /usr/local/etc/my.cnf ~/.my.cnf</pre>
​
<p>デフォだと&uarr;な感じで左から読み込まれます。
	<br>今回は~/.my.cnfを作成する感じにします。</p>
​
<h2>2:my.cnfに追記する</h2><pre>$ vi ~/.my.cnf
[mysqld_safe]
timezone = UTC</pre>
​
<p>初めて編集する場合は真っ白けなので&uarr;の2行だけ追記します。</p>
​
<h2>3:MySQL再起動</h2><pre>$ mysql.server restart
Shutting down MySQL
. SUCCESS!
Starting MySQL
. SUCCESS!</pre>
​
<h2>4:ちゃんと変更されたかMySQLで確認</h2><pre>$ mysql
mysql&gt; show variables like &#39;%time_zone%&#39;;
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | UTC    |
| time_zone        | SYSTEM |
+------------------+--------+</pre>
​
<p>こんなかんじでお手軽です。
	<br>元に戻す際は~/.my.cnfのファイルを削除してMySQLを再起動することで戻ります。</p>
​
<h3>小ネタ</h3><pre>$ mysql
ERROR 2002 (HY000): Can&#39;t connect to local MySQL server through socket &#39;/tmp/mysql.sock&#39; (2)</pre>
​
<p>こんなかんじのエラーが出てmysqlに繋がらない事があります。
	<br>こんな時はpsで起動中のmysqlを探してkillすると良いかもです。</p><pre>$ ps aux | grep mysqld
sample 18491   0.0  2.8  3122552 464132   ??  S     9:18PM   0:09.36 /usr/local/Cellar/mysql/5.6.26/bin/mysqld --basedir=/usr/local/Cellar/mysql/5.6.26 --datadir=/usr/local/var/mysql --plugin-dir=/usr/local/Cellar/mysql/5.6.26/lib/plugin --bind-address=127.0.0.1
sample 18393   0.0  0.0  2461020   1120   ??  S     9:18PM   0:00.02 /bin/sh /usr/local/opt/mysql/bin/mysqld_safe --bind-address=127.0.0.1 --datadir=/usr/local/var/mysql
sample 26587   0.0  0.0  2423356    208 s016  R+   10:18AM   0:00.00 grep mysqld
$ kill -KILL 18491</pre>
​
<p>HomebrewでMySQLをインストール時にLaunchAgentsにplistファイルを登録してると自動的に起動してくれると思います。</p>