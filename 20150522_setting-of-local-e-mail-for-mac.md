# Macな開発でローカル配信メールを設定

<div><p>Macにおいて開発する際に結構困るのがメール設定。<br>アカウント登録や通知系で結構利用しますよね。<br>プログラム側の実装はJavaMailなど優秀なライブラリが多数あり記事も結構みかけます。<br>メールを配送する側の記事もルーティングさせる記事は良く見かけますがあえて送信させない記事はそんなになかったのでまとめてみました。</p><h2>環境</h2><p>OSX Yosemite 10.10.3<br>Postfix 2.11.0</p><h2>設定</h2><h4>transport_mapsの作成</h4><pre class="hljs ruby"><span class="hljs-variable">$ </span>sudo vi /etc/postfix/transport_maps

<span class="hljs-comment"># 下記内容を追記</span>
/^.*@.*<span class="hljs-variable">$/</span> local
</pre><h4>aliases.dbの作成と設定の適用</h4><pre class="hljs ruby"><span class="hljs-variable">$ </span>sudo postalias /etc/postfix/aliases
<span class="hljs-variable">$ </span>sudo newaliases
</pre><h4>main.cfの書き換え</h4><pre class="hljs makefile">$ sudo vi /etc/postfix/main.cf

<span class="hljs-comment"># 未指定のlocal_recipient_mapsを追記</span>
<span class="hljs-comment">#local_recipient_maps =</span>
↓
<span class="hljs-comment">#local_recipient_maps =</span>
<span class="hljs-constant">local_recipient_maps</span> =

<span class="hljs-comment"># postfix内のaliasesを指定</span>
<span class="hljs-comment">#alias_maps = netinfo:/aliases</span>
↓
<span class="hljs-comment">#alias_maps = netinfo:/aliases</span>
<span class="hljs-constant">alias_maps</span> = hash:/etc/postfix/aliases

<span class="hljs-comment"># postfix内のaliasesを指定</span>
<span class="hljs-comment">#alias_database = hash:/etc/aliases, hash:/opt/majordomo/aliases</span>
↓
<span class="hljs-comment">#alias_database = hash:/etc/aliases, hash:/opt/majordomo/aliases</span>
<span class="hljs-constant">alias_database</span> = hash:/etc/postfix/aliases

<span class="hljs-comment"># メールボックスタイプに指定</span>
<span class="hljs-comment">#home_mailbox = Mailbox</span>
↓
<span class="hljs-comment">#home_mailbox = Mailbox</span>
<span class="hljs-constant">home_mailbox</span> = Maildir/

<span class="hljs-comment"># 知らないアドレスに対するメールを転送するユーザーを指定</span>
<span class="hljs-comment">#luser_relay = admin+$local</span>
↓
<span class="hljs-comment">#luser_relay = admin+$local</span>
<span class="hljs-constant">luser_relay</span> = okumura

<span class="hljs-comment">#先ほど作成したtransport_mapsを指定</span>
<span class="hljs-comment"># transport_mapsは既存のconf内では使われていないので最下行に追記</span>
<span class="hljs-constant">transport_maps</span> = pcre:/etc/postfix/transport_maps
</pre><p>これでJavaMailなどから25ポート向けにメールが発送された場合に自動的に/Users/okumura/Maildirへすべて転送されます。<br>transport_mapsの内容がその他のドメインに対するメールの設定になってます。<br></p><h3>おまけ</h3><h5>諸々のメールコマンド</h5><pre class="hljs ruby"><span class="hljs-comment"># postfix起動</span>
<span class="hljs-variable">$ </span>sudo /usr/sbin/postfix start

<span class="hljs-comment"># postfix再起動</span>
<span class="hljs-variable">$ </span>sudo /usr/sbin/postfix reload

<span class="hljs-comment"># メールキュー一覧表示</span>
<span class="hljs-variable">$ </span>mailq

<span class="hljs-comment"># メール内容表示</span>
<span class="hljs-variable">$ </span>sudo postcat -q [キュー<span class="hljs-constant">ID</span>]

<span class="hljs-comment"># メール内容デコード表示(nkf必須)</span>
<span class="hljs-variable">$ </span>sudo postcat -q [キュー<span class="hljs-constant">ID</span>] | nkf -m

<span class="hljs-comment"># メールキュー全削除</span>
<span class="hljs-variable">$ </span>sudo postsuper -d <span class="hljs-constant">ALL</span>

<span class="hljs-comment"># postfixバージョン確認</span>
<span class="hljs-variable">$ </span>postconf mail_version

<span class="hljs-comment"># メール送信確認</span>
<span class="hljs-variable">$ </span>mail [メールアドレス]
<span class="hljs-variable">$ </span><span class="hljs-constant">Subject</span><span class="hljs-symbol">:</span> [件名入力後<span class="hljs-constant">Enter</span>]
<span class="hljs-variable">$ </span>[本文入力後<span class="hljs-constant">Enter</span>]
<span class="hljs-variable">$ </span>[本文入力を終了し送信する場合は <span class="hljs-constant">Ctrl</span> + <span class="hljs-constant">D</span> ]
</pre><h5>ローカルのメールアドレス</h5><p>[ユーザー名]@[PC名].local</p><h5>Telnetを使ったメール送信</h5><pre class="hljs sql">$ telnet localhost 25
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

354 <span class="hljs-operator"><span class="hljs-keyword">End</span> <span class="hljs-keyword">data</span> <span class="hljs-keyword">with</span> &lt;CR&gt;&lt;LF&gt;.&lt;CR&gt;&lt;LF&gt;
subject: <span class="hljs-keyword">test</span> ←件名
<span class="hljs-keyword">from</span>: ken@tagbangers.co.jp ←送信元メールアドレス
<span class="hljs-keyword">to</span>: okumura@tagbangers.co.jp ←送信先メールアドレス
mail <span class="hljs-keyword">test</span> <span class="hljs-keyword">body</span> ←本文
. ←メール終了&amp;送信

<span class="hljs-number">250</span> <span class="hljs-number">2.0</span><span class="hljs-number">.0</span> Ok: queued <span class="hljs-keyword">as</span> F32D559FD77
quit ←telnet終了

<span class="hljs-number">221</span> <span class="hljs-number">2.0</span><span class="hljs-number">.0</span> Bye
<span class="hljs-keyword">Connection</span> closed <span class="hljs-keyword">by</span> foreign host.
</span></pre></div>