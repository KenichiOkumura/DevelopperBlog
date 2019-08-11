# Brewで楽々Javaバージョン切り替え

<p>OSXで開発をガリガリやってるとJDKを複数インストールしたい場合が出てきます。
	<br>最新のしか入れたくないですぅ!っと言ってしまいたい所ですがそうもいかない場合が多いですね。
	<br>そんな際にはHomebrewを利用してインストールするのがオススメです。</p>
​
<h5>まずはbrewにbrew-caskとcaskroom/versionsをインストール</h5><pre>$ brew install brew-cask
$ brew tap caskroom/versions</pre>
​
<h5>続いてcask searchでインストール可能なjavaの種類を検索</h5><pre>$ brew cask search java
==&gt; Exact match
java
==&gt; Partial matches
java6 java7</pre>
​
<h5>インストールしたいjavaバージョンをcaskで指定してインストール&amp;その後バージョン確認</h5><pre>$ brew cask install java7
$ java -version
java version &quot;1.7.0_51&quot;
Java(TM) SE Runtime Environment (build 1.7.0_51-b13)
Java HotSpot(TM) 64-Bit Server VM (build 24.51-b03, mixed mode)</pre>
​
<h5>1.8に戻したい場合は下記コマンドで戻る</h5><pre>$ export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)</pre>
​
<h5>1.7に戻したい場合は下記コマンドで戻る</h5><pre>$ export JAVA_HOME=$(/usr/libexec/java_home -v 1.7)</pre>
​
<p>なお、インストールされる場所は下記の通りです。</p><pre>$ ls /Library/Java/JavaVirtualMachines/</pre>