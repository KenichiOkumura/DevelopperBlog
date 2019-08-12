https://blog.tagbangers.co.jp/ja/2015/05/22/setting-of-local-e-mail-for-mac

# Macな開発でローカル配信メールを設定
Macにおいて開発する際に結構困るのがメール設定。
アカウント登録や通知系で結構利用しますよね。
プログラム側の実装はJavaMailなど優秀なライブラリが多数あり記事も結構みかけます。
メールを配送する側の記事もルーティングさせる記事は良く見かけますがあえて送信させない記事はそんなになかったのでまとめてみました。

## 環境
OSX Yosemite 10.10.3
Postfix 2.11.0
## 設定
### transport_mapsの作成
```
$ sudo vi /etc/postfix/transport_maps

# 下記内容を追記
/^.*@.*$/ local
```

### aliases.dbの作成と設定の適用
```
$ sudo postalias /etc/postfix/aliases
$ sudo newaliases
```

### main.cfの書き換え
```
$ sudo vi /etc/postfix/main.cf

# 未指定のlocal_recipient_mapsを追記
#local_recipient_maps =
↓
#local_recipient_maps =
local_recipient_maps =

# postfix内のaliasesを指定
#alias_maps = netinfo:/aliases
↓
#alias_maps = netinfo:/aliases
alias_maps = hash:/etc/postfix/aliases

# postfix内のaliasesを指定
#alias_database = hash:/etc/aliases, hash:/opt/majordomo/aliases
↓
#alias_database = hash:/etc/aliases, hash:/opt/majordomo/aliases
alias_database = hash:/etc/postfix/aliases

# メールボックスタイプに指定
#home_mailbox = Mailbox
↓
#home_mailbox = Mailbox
home_mailbox = Maildir/

# 知らないアドレスに対するメールを転送するユーザーを指定
#luser_relay = admin+$local
↓
#luser_relay = admin+$local
luser_relay = okumura

#先ほど作成したtransport_mapsを指定
# transport_mapsは既存のconf内では使われていないので最下行に追記
transport_maps = pcre:/etc/postfix/transport_maps
```

これでJavaMailなどから25ポート向けにメールが発送された場合に自動的に/Users/okumura/Maildirへすべて転送されます。
transport_mapsの内容がその他のドメインに対するメールの設定になってます。

## おまけ
### 諸々のメールコマンド
```
# postfix起動
$ sudo /usr/sbin/postfix start

# postfix再起動
$ sudo /usr/sbin/postfix reload

# メールキュー一覧表示
$ mailq

# メール内容表示
$ sudo postcat -q [キューID]

# メール内容デコード表示(nkf必須)
$ sudo postcat -q [キューID] | nkf -m

# メールキュー全削除
$ sudo postsuper -d ALL

# postfixバージョン確認
$ postconf mail_version

# メール送信確認
$ mail [メールアドレス]
$ Subject: [件名入力後Enter]
$ [本文入力後Enter]
$ [本文入力を終了し送信する場合は Ctrl + D ]
```

### ローカルのメールアドレス
[ユーザー名]@[PC名].local

### Telnetを使ったメール送信
```
$ telnet localhost 25
Trying ::1...
Connected to localhost.
Escape character is '^]'.
220 mbp-pc.local ESMTP Postfix
HELO localhost ←ドメイン名は適当でOK

250 mbp-pc.local
MAIL FROM:ken@tagbangers.co.jp ←送信元メールアドレス

250 2.1.0 Ok
RCPT TO:okumura@tagbangers.co.jp ←送信先メールアドレス

250 2.1.5 Ok
DATA ←メール内容の記載開始を通知

354 End data with <CR><LF>.<CR><LF>
subject: test ←件名
from: ken@tagbangers.co.jp ←送信元メールアドレス
to: okumura@tagbangers.co.jp ←送信先メールアドレス
mail test body ←本文
. ←メール終了&送信

250 2.0.0 Ok: queued as F32D559FD77
quit ←telnet終了

221 2.0.0 Bye
Connection closed by foreign host.
```