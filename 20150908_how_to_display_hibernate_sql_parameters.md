https://blog.tagbangers.co.jp/ja/2015/09/08/how_to_display_hibernate_sql_parameters

# Hibernateで実行されたSQLとパラメータのログを出す

Hibernateで開発を行っている時に実際にSQLってどうやって実行されてるんだ?っと思ったりします。
そんな時にはlogback.xmlに下記のタグを追加してみてください。
```
<logger name="org.hibernate.SQL" level="DEBUG" />
<logger name="org.hibernate.type.descriptor.sql.BasicBinder" level="TRACE" />
```
そしたら下記な感じで出力されます。
```
12:10:02.883 [http-nio-8081-exec-4] DEBUG org.hibernate.SQL:109 - select sample0_.id as id1_11_ from sample sample0_ where sample0_.id=? and sample0_.type=? and sample0_.create_date>=?
12:10:02.883 [http-nio-8081-exec-4] TRACE o.h.type.descriptor.sql.BasicBinder:81 - binding parameter [1] as [INTEGER] - [4]
12:10:02.884 [http-nio-8081-exec-4] TRACE o.h.type.descriptor.sql.BasicBinder:81 - binding parameter [2] as [VARCHAR] - [summary]
12:10:02.885 [http-nio-8081-exec-4] TRACE o.h.type.descriptor.sql.BasicBinder:81 - binding parameter [3] as [TIMESTAMP] - [2015-01-01]
12:10:02.885 [http-nio-8081-exec-4] TRACE o.h.type.descriptor.sql.BasicBinder:81 - binding parameter [3] as [TIMESTAMP] - [2015-01-01 09:00:00.0]
```
SQL表示するまでは結構すぐに見つかるんですがパラメータまで出力するのを検索するのに結構手間取ってしまった...。