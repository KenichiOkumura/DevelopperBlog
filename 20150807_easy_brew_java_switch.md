https://blog.tagbangers.co.jp/ja/2015/08/07/Brewで楽々Javaバージョン切り替え

# Brewで楽々Javaバージョン切り替え

OSXで開発をガリガリやってるとJDKを複数インストールしたい場合が出てきます。
最新のしか入れたくないですぅ!っと言ってしまいたい所ですがそうもいかない場合が多いですね。
そんな際にはHomebrewを利用してインストールするのがオススメです。
​
## まずはbrewにbrew-caskとcaskroom/versionsをインストール
```
$ brew install brew-cask
$ brew tap caskroom/versions
```
​
## 続いてcask searchでインストール可能なjavaの種類を検索
```
$ brew cask search java
==> Exact match
java
==> Partial matches
java6 java7
```
​
## インストールしたいjavaバージョンをcaskで指定してインストール&その後バージョン確認
```
$ brew cask install java7
$ java -version
java version '1.7.0_51'
Java(TM) SE Runtime Environment (build 1.7.0_51-b13)
Java HotSpot(TM) 64-Bit Server VM (build 24.51-b03, mixed mode)
```
​
## 1.8に戻したい場合は下記コマンドで戻る
```
$ export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
```
​
## 1.7に戻したい場合は下記コマンドで戻る
```
$ export JAVA_HOME=$(/usr/libexec/java_home -v 1.7)
```
​
なお、インストールされる場所は下記の通りです。
```
$ ls /Library/Java/JavaVirtualMachines/
```