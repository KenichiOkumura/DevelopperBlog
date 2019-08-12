https://blog.tagbangers.co.jp/ja/2015/12/03/Xcode_library_not_found_for_marumaru

# Xcodeで「ld: library not found for -l○○」が出続ける

iOSの開発をしている方に取っては馴染み深い「CocoaPods」ですがこれにまつわるエラーにとてもとてもハマったので備忘録しておきます。

```
ld: library not found for -lPods
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

CocoaPodsを利用した開発をしている際にまれにタイトルにある「ld: library not found for -l○○」というエラーが発生します。
これは○○に当てはまるライブラリが読み込めず、コンパイルに失敗した際に発生します。
単純にここだけ考えるとライブラリが存在していないだけか、ライブラリへのリンクが間違っているので修正すれば治りそうなものです。

実際にこのエラーでGoogle先生にお尋ねするとおおよそ
・CocoaPodsをinstallし直す
・libPods.aをLink Binary With Librariesから削除→再追加する
・Manage SchemeからPodsプロジェクトのShareにチェックを入れる
と言った辺りの対策が見つかります。

見つかった対策を全て試しても上手く動かない。
でも別の人は動いている...?

そんな方は
Edit Schemes &gt; Build
を確認してみてください。
![1.png](/20151203_Xcode_library_not_found_for_marumaru/1.png)

ここにPodsプロジェクトを追加してClean → Buildしたところ見事動きました...!
設定によっては更にTarget BuildSettingsのBuild Active Architecture OnlyをYesにしないと動作しないかもしれませんのでお気をつけ下さい。

まさかこんな初歩的なところでミスってるとは思いもせず、とは言え見逃しやすいところかも知れません...。
同じような現象で悩んでいる方は一度ご確認してみてはいかがでしょう??