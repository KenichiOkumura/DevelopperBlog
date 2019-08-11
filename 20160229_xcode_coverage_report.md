# Xcode7.0環境下でカバレッジレポートを出力する

<div><p>前回<a href="http://qiita.com/KenichiOkumura@github/items/3a531a78c9b897557c9f">投稿した記事</a>でカバレッジの確認はできるようになりましたが納品などが絡む場合はやはりレポート形式で出力したくなります。<br>
	今回まさにそんな事例に行き当たったので備忘録がてら共有いたします。<br>
	※本記事は2016年02月29日時点での内容となります。
</p><h2>実行環境</h2><ul>
	<li>OSX Yosemite 10.10.5</li>
	<li>Xcode 7.2 (7C68)</li>
	<li>CocoaPods 0.39.0</li>
	<li>Homebrew 0.9.5</li>
</ul><h2>対象となるケース</h2><ul>
	<li>CocoaPodsでパッケージ管理している</li>
	<li>Unitテストを書いている</li>
	<li>カバレッジレポートをHTMLで出力したい</li>
</ul><h2>利用するツール等々</h2><ul>
	<li><a href="https://github.com/jonreid/XcodeCoverage">XcodeCoverage</a></li>
	<li><a href="http://ltp.sourceforge.net/coverage/lcov.php">lcov</a></li>
	<li><a href="https://www.gnu.org/software/sed/">gnu-sed</a></li>
</ul><h2>対象プロジェクト</h2><p><a href="https://github.com/KenichiOkumura/CoverageReportSample.git">https://github.com/KenichiOkumura/CoverageReportSample.git</a><br>
	こちらのプロジェクトは下記の手順で作成されています。
</p><ul>
	<li>Wellcome to Xcode &gt; Create a new Xcode project</li>
	<li>iOS &gt; Application &gt; Single View Application</li>
	<li>各種設定は下記な感じ<br>
	<img alt="image" src="https://s3-ap-northeast-1.amazonaws.com/qiita/2/26d8f56d-25ba-496d-a78a-8341532cd281.png"></li>
	<li>TargetClass.h TargetClass.m 追加&amp;編集</li>
	<li>CoverageReportSampleTests.m 編集</li>
	<li>Project &gt; CoverageReportSample &gt; Generate Legacy Test Coverate Files &gt; YES<br>
	<img alt="image" src="https://s3-ap-northeast-1.amazonaws.com/qiita/2/7605099f-6cb6-4ab1-b55a-55a8a33b684c.png"></li>
	<li>Project &gt; CoverageReportSample &gt; Instrument Program Flow &gt; YES<br>
	<img alt="image" src="https://s3-ap-northeast-1.amazonaws.com/qiita/2/1ec03fb5-a79f-46cb-a6e2-fdf01377adff.png"></li>
	<li>TARGETS &gt; Build Phases &gt; + &gt; New Run Script Phase &gt; Pods/XcodeCoverage/exportenv.sh<br>
	<img alt="image" src="https://s3-ap-northeast-1.amazonaws.com/qiita/2/d44b5c3e-c327-4fdc-8c17-23a0fb9ca67e.png"></li>
	<li>pod init &gt; PodfileにXcodeCoverage追加</li>
</ul><h2>レポート生成手順</h2><h3>1.Homebrewでlcovをインストール&amp;パス確認</h3><div class="codehilite">
	<pre class="hljs sql">$ brew <span class="hljs-operator"><span class="hljs-keyword">install</span> lcov
==&gt; Downloading <a class="vglnk" href="https://homebrew.bintray.com/bottles/lcov-" rel="nofollow"><span>https</span><span>://</span><span>homebrew</span><span>.</span><span>bintray</span><span>.</span><span>com</span><span>/</span><span>bottles</span><span>/</span><span>lcov</span><span>-</span></a><span class="hljs-number">1.12</span>.yosemite.bottle.tar.gz
Already downloaded: /<span class="hljs-keyword">Library</span>/Caches/Homebrew/lcov-<span class="hljs-number">1.12</span>.yosemite.bottle.tar.gz
==&gt; Pouring lcov-<span class="hljs-number">1.12</span>.yosemite.bottle.tar.gz
  /usr/<span class="hljs-keyword">local</span>/Cellar/lcov/<span class="hljs-number">1.12</span>: <span class="hljs-number">16</span> files, <span class="hljs-number">533.3</span><span class="hljs-keyword">K</span>
$ which lcov
/usr/<span class="hljs-keyword">local</span>/<span class="hljs-keyword">bin</span>/lcov
$ lcov <span class="hljs-comment">--version</span>
lcov: LCOV <span class="hljs-keyword">version</span> <span class="hljs-number">1.12</span>
    </span></pre>
</div><h3>2.pod install</h3><div class="codehilite">
	<pre class="hljs sql">$ cd {PROJECT_ROOT}
$ pod <span class="hljs-operator"><span class="hljs-keyword">install</span>
Updating <span class="hljs-keyword">local</span> specs repositories
CocoaPods <span class="hljs-number">1.0</span><span class="hljs-number">.0</span>.beta<span class="hljs-number">.4</span> <span class="hljs-keyword">is</span> available.
<span class="hljs-keyword">To</span> <span class="hljs-keyword">update</span> <span class="hljs-keyword">use</span>: <span class="hljs-string">`gem install cocoapods --pre`</span>
[!] This <span class="hljs-keyword">is</span> a <span class="hljs-keyword">test</span> <span class="hljs-keyword">version</span> we<span class="hljs-string">'d love you to try.
For more information see <a class="vglnk" href="http://blog.cocoapods.org" rel="nofollow"><span>http</span><span>://</span><span>blog</span><span>.</span><span>cocoapods</span><span>.</span><span>org</span></a>
and the CHANGELOG for this version <a class="vglnk" href="http://git.io/BaH8pQ" rel="nofollow"><span>http</span><span>://</span><span>git</span><span>.</span><span>io</span><span>/</span><span>BaH8pQ</span></a>.
Analyzing dependencies
Downloading dependencies
Installing XcodeCoverage (1.2.2)
Generating Pods project
Integrating client project
Sending stats
Pod installation complete! There is 1 dependency from the Podfile and 1 total pod installed.
    </span></span></pre>
</div><h3>3.envcov.shの中身をbrewでインストールしたlcovのパスに書き換え</h3><p>CocoaPodsに取得したXcodeCoverage内のenvcov.shに記載されているlcovの実行パスをHomebrewでインストールしたものに書き換えます。<br>
	この記事を書いている時点でのenvcov.shではXcodeCoverageに内蔵されているlcov-1.11で実行するように書かれていますがXcode7環境では上手く動作しませんでした(<a href="http://stackoverflow.com/questions/32912030/xcode7-code-coverage-with-getcov-and-lcov">参考</a>)。
</p><div class="codehilite">
	<pre class="hljs bash">$ <span class="hljs-built_in">cd</span> {PROJECT_ROOT}
$ vi Pods/XcodeCoverage/envcov.sh
<span class="hljs-number">8</span> - LCOV_PATH=<span class="hljs-string">"<span class="hljs-variable">${scripts}</span>/lcov-1.11/bin"</span>
<span class="hljs-number">8</span> + LCOV_PATH=<span class="hljs-string">"/usr/local/bin/"</span>
    </pre>
</div><h3>4.テスト実行</h3><p>CoverageReportSample.xcworkspaceを開きテストを実行します。
	<em> CoverageReportSample.xcworkspaceを開く
	</em> CoverageReportSample &gt; 適当なエミュレーターを選択 &gt; Product &gt; Test
</p><h3>5.XcodeCoverage実行</h3><p>CocoaPodsに取得したXcodeCoverage内のgetcovを実行します。
</p><div class="codehilite">
	<pre class="hljs sql">$ cd {PROJECT_ROOT}
$ ./Pods/XcodeCoverage/getcov <span class="hljs-comment">--show -o ~/Desktop/</span>
<span class="hljs-operator"><span class="hljs-keyword">Show</span> HTML Report
output_dir = /<span class="hljs-keyword">Users</span>/<span class="hljs-keyword">user</span>/Desktop/
~/Desktop ~/Desktop/CoverageReportSample
~/Desktop/CoverageReportSample
Capturing coverage <span class="hljs-keyword">data</span> <span class="hljs-keyword">from</span> /<span class="hljs-keyword">Users</span>/<span class="hljs-keyword">user</span>/<span class="hljs-keyword">Library</span>/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/<span class="hljs-keyword">Build</span>/Intermediates/CoverageReportSample.<span class="hljs-keyword">build</span>/Debug-iphonesimulator/CoverageReportSample.<span class="hljs-keyword">build</span>/Objects-<span class="hljs-keyword">normal</span>/x86_64
<span class="hljs-keyword">Found</span> gcov <span class="hljs-keyword">version</span>: <span class="hljs-number">7.0</span><span class="hljs-number">.2</span>
<span class="hljs-keyword">Found</span> LLVM gcov <span class="hljs-keyword">version</span> <span class="hljs-number">3.4</span>, which emulates gcov <span class="hljs-keyword">version</span> <span class="hljs-number">4.2</span>
Scanning /<span class="hljs-keyword">Users</span>/<span class="hljs-keyword">user</span>/<span class="hljs-keyword">Library</span>/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/<span class="hljs-keyword">Build</span>/Intermediates/CoverageReportSample.<span class="hljs-keyword">build</span>/Debug-iphonesimulator/CoverageReportSample.<span class="hljs-keyword">build</span>/Objects-<span class="hljs-keyword">normal</span>/x86_64 <span class="hljs-keyword">for</span> .gcda files ...
<span class="hljs-keyword">Found</span> <span class="hljs-number">4</span> <span class="hljs-keyword">data</span> files <span class="hljs-keyword">in</span> /<span class="hljs-keyword">Users</span>/<span class="hljs-keyword">user</span>/<span class="hljs-keyword">Library</span>/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/<span class="hljs-keyword">Build</span>/Intermediates/CoverageReportSample.<span class="hljs-keyword">build</span>/Debug-iphonesimulator/CoverageReportSample.<span class="hljs-keyword">build</span>/Objects-<span class="hljs-keyword">normal</span>/x86_64
Processing x86_64/AppDelegate.gcda
Processing x86_64/<span class="hljs-keyword">main</span>.gcda
Processing x86_64/TargetClass.gcda
Processing x86_64/ViewController.gcda
Finished .info-<span class="hljs-keyword">file</span> <span class="hljs-keyword">creation</span>
Reading tracefile Coverage.info
Deleted <span class="hljs-number">0</span> files
Writing <span class="hljs-keyword">data</span> <span class="hljs-keyword">to</span> Coverage.info
Summary coverage rate:
  <span class="hljs-keyword">lines</span>......: <span class="hljs-number">64.0</span>% (<span class="hljs-number">16</span> <span class="hljs-keyword">of</span> <span class="hljs-number">25</span> <span class="hljs-keyword">lines</span>)
  functions..: <span class="hljs-number">60.0</span>% (<span class="hljs-number">9</span> <span class="hljs-keyword">of</span> <span class="hljs-number">15</span> functions)
  branches...: <span class="hljs-keyword">no</span> <span class="hljs-keyword">data</span> <span class="hljs-keyword">found</span>
Reading tracefile Coverage.info
Removing /<span class="hljs-keyword">Users</span>/<span class="hljs-keyword">user</span>/Desktop/CoverageReportSample/CoverageReportSample/<span class="hljs-keyword">main</span>.<span class="hljs-keyword">m</span>
Deleted <span class="hljs-number">1</span> files
Writing <span class="hljs-keyword">data</span> <span class="hljs-keyword">to</span> Coverage.info
Summary coverage rate:
  <span class="hljs-keyword">lines</span>......: <span class="hljs-number">57.1</span>% (<span class="hljs-number">12</span> <span class="hljs-keyword">of</span> <span class="hljs-number">21</span> <span class="hljs-keyword">lines</span>)
  functions..: <span class="hljs-number">57.1</span>% (<span class="hljs-number">8</span> <span class="hljs-keyword">of</span> <span class="hljs-number">14</span> functions)
  branches...: <span class="hljs-keyword">no</span> <span class="hljs-keyword">data</span> <span class="hljs-keyword">found</span>
Reading <span class="hljs-keyword">data</span> <span class="hljs-keyword">file</span> Coverage.info
<span class="hljs-keyword">Found</span> <span class="hljs-number">4</span> entries.
<span class="hljs-keyword">Found</span> common filename prefix <span class="hljs-string">"/Users/user/Desktop/CoverageReportSample"</span>
Writing .css <span class="hljs-keyword">and</span> .png files.
Generating <span class="hljs-keyword">output</span>.
Processing <span class="hljs-keyword">file</span> CoverageReportSample/ViewController.<span class="hljs-keyword">m</span>
Processing <span class="hljs-keyword">file</span> CoverageReportSample/TargetClass.<span class="hljs-keyword">m</span>
Processing <span class="hljs-keyword">file</span> CoverageReportSample/AppDelegate.h
Processing <span class="hljs-keyword">file</span> CoverageReportSample/AppDelegate.<span class="hljs-keyword">m</span>
Writing <span class="hljs-keyword">directory</span> <span class="hljs-keyword">view</span> page.
Overall coverage rate:
  <span class="hljs-keyword">lines</span>......: <span class="hljs-number">57.1</span>% (<span class="hljs-number">12</span> <span class="hljs-keyword">of</span> <span class="hljs-number">21</span> <span class="hljs-keyword">lines</span>)
  functions..: <span class="hljs-number">57.1</span>% (<span class="hljs-number">8</span> <span class="hljs-keyword">of</span> <span class="hljs-number">14</span> functions)
    </span></pre>
</div><h2>あとがき</h2><p>結果はこんな感じにできあがります。<br>
	通っていない所は赤く表示され非常にわかりやすいですね!
	<img alt="image" src="https://s3-ap-northeast-1.amazonaws.com/qiita/2/cadaef8a-9a4a-4aee-bc38-6550812ec837.png">
</p><p>なお、Pod内で書き換えているenvcov.shは当然の事ながらPodが更新されると消える可能性があります。<br>
	自分は手間だったのでgnu-sedで置換するようにスクリプト作りました。
</p><div class="codehilite">
	<pre class="hljs bash">$ <span class="hljs-built_in">cd</span> {PROJECT_ROOT}
$ touch coverage.sh
$ chmod +x coverage.sh
$ vi coverage.sh
<span class="hljs-shebang">#!/bin/bash</span>
<span class="hljs-comment"># brewでlcoveとgnu-sedをインストール</span>
brew install lcove gnu-sed
<span class="hljs-comment"># brew でのインストール先確認</span>
<span class="hljs-comment"># which lcov</span>
<span class="hljs-comment"># envcov.shのlcov参照先をbrewへ向ける</span>
gsed -i <span class="hljs-string">'8c LCOV_PATH="/usr/local/bin/"'</span> Pods/XcodeCoverage/envcov.sh
<span class="hljs-comment"># カバレッジレポートをデスクトップへ出力</span>
./Pods/XcodeCoverage/getcov --show -o ~/Desktop/
    </pre>
</div></div>