# CocoaPods管理下のプロジェクトをUniversal Static Libraryとして作成する

<div><p>Cocoapodsを利用しているプロジェクトをStatic Libraryとして出力する際の手法の小ネタです。<br>
結論から書くと<a href="https://github.com/CocoaPods/cocoapods-packager">cocoapods-packager</a>を利用すれば一撃です。</p><p>Static Libraryを作成するにはxcodebuildを利用しRunScriptとかにスクリプト書いて実行するのがベターです。<br>
この辺りはググると山程出るのでそちらにお任せします。</p><p>今回はそんな中でCocoapodsを利用している場合です。<br>
Cocoapodsを利用していてもxcodebuildを使って出力することは可能でしたがもっと簡単な手法があったのでご紹介です。<br>
<a href="https://github.com/CocoaPods/cocoapods-packager">cocoapods-packager</a><br>
<a href="https://guides.cocoapods.org/syntax/podspec.html">podspec</a>を記載する事でその内容をベースにStatic Libraryを作成してくれるライブラリです。
導入〜実行もpodspecファイルを作成し、gemで入れて追加されたpod packageを呼び出すだけ!</p><div class="codehilite"><pre class="hljs ruby"><span class="hljs-variable">$ </span>cd <span class="hljs-variable">${</span><span class="hljs-constant">PROJECT_ROOT</span>}
<span class="hljs-variable">$ </span>gem install cocoapods-packager
<span class="hljs-variable">$ </span>pod package <span class="hljs-constant">Project</span>.podspec
</pre></div><p>後は実行したディレクトリに作成されたproject.frameworkを利用するだけです。<br>
非常に簡単ですね。</p><p>ハマった点としてはpodspecファイルにspec.sourceの項目が記載されていないとrubyのエラーが表示されます。<br>
パット見rubyのバージョンとかの絡みか!?とか思ってしまい時間がかかりました...。<br>
ローカルのリポジトリしか無い場合でも下記な感じで記載すればOKでした。</p><div class="codehilite"><pre class="hljs php">spec.source = { :git =&gt; <span class="hljs-string">'/Users/sample/Project'</span>, :tag =&gt; <span class="hljs-string">'develop'</span> }
</pre></div><p>プロジェクト中でCocoapodsを利用し、参照している場合も良きに計らってくれました。<br>
皆様も是非お試しくださいませー</p></div>