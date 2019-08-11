# Thymeleafでpomのversionを利用する

<div><p>お久しぶりです。奥村です。<br>GWを明日に控えたこのタイミングで連休ボケする前に小ネタを1つ投稿しておきます。<br>pomのversion値を利用して、各バージョンごとでcssファイルなどのキャッシュをリセットさせたい！っといった要望があった際に利用する小ネタです。</p><p>pom.xml</p><pre class="hljs xml"><span class="hljs-tag">&lt;<span class="hljs-title">project</span>&gt;</span>
&nbsp; &nbsp; <span class="hljs-tag">&lt;<span class="hljs-title">modelversion</span>&gt;</span>4.0.0<span class="hljs-tag">&lt;/<span class="hljs-title">modelversion</span>&gt;</span>
&nbsp; &nbsp; <span class="hljs-tag">&lt;<span class="hljs-title">groupid</span>&gt;</span>com.example<span class="hljs-tag">&lt;/<span class="hljs-title">groupid</span>&gt;</span>
&nbsp; &nbsp; <span class="hljs-tag">&lt;<span class="hljs-title">artifactid</span>&gt;</span>sample<span class="hljs-tag">&lt;/<span class="hljs-title">artifactid</span>&gt;</span>
&nbsp; &nbsp; <span class="hljs-tag">&lt;<span class="hljs-title">version</span>&gt;</span>1.0.0.RELEASE<span class="hljs-tag">&lt;/<span class="hljs-title">version</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">project</span>&gt;</span></pre><p>application.properties</p><pre class="hljs coffeescript">pom.version=<span class="hljs-property">@project</span>.version@
</pre><p>index.html</p><pre class="hljs xml"><span class="hljs-tag">&lt;<span class="hljs-title">p</span> <span class="hljs-attribute">th:text</span>=<span class="hljs-value">"${@environment.getProperty('pom.version')}"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">p</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">p</span> <span class="hljs-attribute">th:text</span>=<span class="hljs-value">"${@environment.getProperty('pom.version').hashCode()}"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">p</span>&gt;</span>

1.0.0.RELEASE
-1138007634
</pre><p>pomのバージョンをそのまま使うのはあまりよろしくない場合はObject.hashCode()等を利用してハッシュ値にしてしまえば利用しやすいと思います。<br>Apache Commons Codec の DigestUtils などを利用するのも手ですね。<br>また、同一バージョン値での開発中の場合は結局キャッシュが効いてしまうのでビルド単位でバージョン番号を発行したししたかったですが連休前なので今回はこれぐらいで…。</p></div>