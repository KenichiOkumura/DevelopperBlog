# Dockerでmysqlを建てた際に文字コードをよしなにする

<div><p>連投です。奥村です。<br>最近弊社ではdocker推しなのでビッグウェーブに乗る意味も兼ねて小ネタを。</p><p>dockerでmysqlを立てる場合の超簡易なコマンドは下記の通り。</p><pre class="hljs bash">$ docker run <span class="hljs-operator">-d</span> --name mysql <span class="hljs-operator">-e</span> MYSQL_ROOT_PASSWORD=password -p <span class="hljs-number">3306</span>:<span class="hljs-number">3306</span> mysql</pre><p>上のコマンドで立ち上げたmysqlでデータベースを作成して文字コード確認してみると下記の通り。</p><pre class="hljs sql">~ $ docker exec -it mysql bash
root@501cbebbcdf3:/# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor. &nbsp;Commands <span class="hljs-operator"><span class="hljs-keyword">end</span> <span class="hljs-keyword">with</span> ;</span> or \g.
Your MySQL connection id is 12
Server version: 5.7.17 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type '<span class="hljs-operator"><span class="hljs-keyword">help</span>;</span>' or '\h' for <span class="hljs-operator"><span class="hljs-keyword">help</span>. <span class="hljs-keyword">Type</span> <span class="hljs-string">'\c'</span> <span class="hljs-keyword">to</span> <span class="hljs-keyword">clear</span> the <span class="hljs-keyword">current</span> <span class="hljs-keyword">input</span> <span class="hljs-keyword">statement</span>.

mysql&gt; <span class="hljs-keyword">show</span> <span class="hljs-keyword">variables</span> <span class="hljs-keyword">like</span> <span class="hljs-string">"chara%"</span>;</span>
+<span class="hljs-comment">--------------------------+----------------------------+</span>
| Variable_name &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| Value &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
+<span class="hljs-comment">--------------------------+----------------------------+</span>
| character_set_client &nbsp; &nbsp; | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_connection | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_database &nbsp; | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_filesystem | binary &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_results &nbsp; &nbsp;| latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_server &nbsp; &nbsp; | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_system &nbsp; &nbsp; | utf8 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_sets_dir &nbsp; &nbsp; &nbsp; | /usr/share/mysql/charsets/ |
+<span class="hljs-comment">--------------------------+----------------------------+</span>
8 rows in <span class="hljs-operator"><span class="hljs-keyword">set</span> (<span class="hljs-number">0.01</span> sec)
</span></pre><p>ありがちなlatin1さん<br>よくある対処法としてはmy.cnfをいじってしまう対応だけどDockerだからいまいち…。<br>そんなときはコンテナ立ち上げ時にオプション値指定してあげるだけで解決します。<br>[--character-set-server=utf8 --collation-server=utf8_unicode_ci]を追加して実行してみます。</p><pre class="hljs sql">~ $ docker run -d <span class="hljs-comment">--name blog -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql --character-set-server=utf8 --collation-server=utf8_unicode_ci</span>
7851f576e101a87791154a3f71120c132fa3a1e06ec608575614e17a318a3644
~ $ docker exec -it blog bash
root@7851f576e101:/# mysql -uroot -p
Enter password:
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
root@7851f576e101:/# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor. &nbsp;Commands <span class="hljs-operator"><span class="hljs-keyword">end</span> <span class="hljs-keyword">with</span> ;</span> or \g.
Your MySQL connection id is 3
Server version: 5.7.17 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type '<span class="hljs-operator"><span class="hljs-keyword">help</span>;</span>' or '\h' for <span class="hljs-operator"><span class="hljs-keyword">help</span>. <span class="hljs-keyword">Type</span> <span class="hljs-string">'\c'</span> <span class="hljs-keyword">to</span> <span class="hljs-keyword">clear</span> the <span class="hljs-keyword">current</span> <span class="hljs-keyword">input</span> <span class="hljs-keyword">statement</span>.

mysql&gt; <span class="hljs-keyword">show</span> <span class="hljs-keyword">variables</span> <span class="hljs-keyword">like</span> <span class="hljs-string">"chara%"</span>;</span>
+<span class="hljs-comment">--------------------------+----------------------------+</span>
| Variable_name &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| Value &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
+<span class="hljs-comment">--------------------------+----------------------------+</span>
| character_set_client &nbsp; &nbsp; | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_connection | latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_database &nbsp; | utf8 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_filesystem | binary &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_results &nbsp; &nbsp;| latin1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_server &nbsp; &nbsp; | utf8 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_set_system &nbsp; &nbsp; | utf8 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |
| character_sets_dir &nbsp; &nbsp; &nbsp; | /usr/share/mysql/charsets/ |
+<span class="hljs-comment">--------------------------+----------------------------+</span>
8 rows in <span class="hljs-operator"><span class="hljs-keyword">set</span> (<span class="hljs-number">0.00</span> sec)
</span></pre><p>Good by latin1!</p></div>