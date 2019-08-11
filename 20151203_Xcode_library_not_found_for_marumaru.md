# Xcodeで「ld: library not found for -l○○」が出続ける

<div><p>iOSの開発をしている方に取っては馴染み深い「CocoaPods」ですがこれにまつわるエラーにとてもとてもハマったので備忘録しておきます。
</p><pre class="hljs bash">ld: library not found <span class="hljs-keyword">for</span> <span class="hljs-operator">-l</span>Pods
clang: error: linker <span class="hljs-built_in">command</span> failed with <span class="hljs-built_in">exit</span> code <span class="hljs-number">1</span> (use -v to see invocation)
</pre><p>CocoaPodsを利用した開発をしている際にまれにタイトルにある「ld: library not found for -l○○」というエラーが発生します。<br>
	これは○○に当てはまるライブラリが読み込めず、コンパイルに失敗した際に発生します。<br>
	単純にここだけ考えるとライブラリが存在していないだけか、ライブラリへのリンクが間違っているので修正すれば治りそうなものです。<br>
</p><p>
	実際にこのエラーでGoogle先生にお尋ねするとおおよそ<br>
	・CocoaPodsをinstallし直す<br>
	・libPods.aをLink Binary With Librariesから削除→再追加する<br>
	・Manage SchemeからPodsプロジェクトのShareにチェックを入れる<br>
	と言った辺りの対策が見つかります。<br>
</p><p>
	見つかった対策を全て試しても上手く動かない。<br>
	でも別の人は動いている...?<br>
	<br>
	そんな方は<br>
	Edit Schemes &gt; Build<br>
	を確認してみてください。<br>
</p><p><img src="/20151203_Xcode_library_not_found_for_marumaru/1.png">
</p><p>
	ここにPodsプロジェクトを追加してClean → Buildしたところ見事動きました...!<br>
	設定によっては更にTarget BuildSettingsのBuild Active Architecture OnlyをYesにしないと動作しないかもしれませんのでお気をつけ下さい。<br>
	<br>
	まさかこんな初歩的なところでミスってるとは思いもせず、とは言え見逃しやすいところかも知れません...。<br>
	同じような現象で悩んでいる方は一度ご確認してみてはいかがでしょう??
</p></div>