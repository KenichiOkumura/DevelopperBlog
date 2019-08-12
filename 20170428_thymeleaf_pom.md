https://blog.tagbangers.co.jp/ja/2017/04/28/thymeleaf_pom

# Thymeleafでpomのversionを利用する
お久しぶりです。奥村です。
GWを明日に控えたこのタイミングで連休ボケする前に小ネタを1つ投稿しておきます。
pomのversion値を利用して、各バージョンごとでcssファイルなどのキャッシュをリセットさせたい！っといった要望があった際に利用する小ネタです。

pom.xml
```
<project>
    <modelversion>4.0.0</modelversion>
    <groupid>com.example</groupid>
    <artifactid>sample</artifactid>
    <version>1.0.0.RELEASE</version>
</project>
```

application.properties
```
pom.version=@project.version@
```

index.html
```
<p th:text="${@environment.getProperty('pom.version')}"></p>
<p th:text="${@environment.getProperty('pom.version').hashCode()}"></p>

1.0.0.RELEASE
-1138007634
```

pomのバージョンをそのまま使うのはあまりよろしくない場合はObject.hashCode()等を利用してハッシュ値にしてしまえば利用しやすいと思います。
Apache Commons Codec の DigestUtils などを利用するのも手ですね。
また、同一バージョン値での開発中の場合は結局キャッシュが効いてしまうのでビルド単位でバージョン番号を発行したししたかったですが連休前なので今回はこれぐらいで…。