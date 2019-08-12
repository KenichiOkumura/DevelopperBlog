https://blog.tagbangers.co.jp/ja/2016/02/29/xcode_coverage_report

#Xcode7.0環境下でカバレッジレポートを出力する

前回[投稿した記事](http://qiita.com/KenichiOkumura@github/items/3a531a78c9b897557c9f)でカバレッジの確認はできるようになりましたが納品などが絡む場合はやはりレポート形式で出力したくなります。
今回まさにそんな事例に行き当たったので備忘録がてら共有いたします。
※本記事は2016年02月29日時点での内容となります。

##実行環境
* OSX Yosemite 10.10.5
* Xcode 7.2 (7C68)
* CocoaPods 0.39.0
* Homebrew 0.9.5

##対象となるケース
* CocoaPodsでパッケージ管理している
* Unitテストを書いている
* カバレッジレポートをHTMLで出力したい

##利用するツール等々
* [XcodeCoverage](https://github.com/jonreid/XcodeCoverage)
* [lcov](http://ltp.sourceforge.net/coverage/lcov.php)
* [gnu-sed](https://www.gnu.org/software/sed/)

##対象プロジェクト
[https://github.com/KenichiOkumura/CoverageReportSample.git](https://github.com/KenichiOkumura/CoverageReportSample.git)
こちらのプロジェクトは下記の手順で作成されています。

* Wellcome to Xcode > Create a new Xcode project
* iOS > Application > Single View Application
* 各種設定は下記な感じ
![image](https://s3-ap-northeast-1.amazonaws.com/qiita/2/26d8f56d-25ba-496d-a78a-8341532cd281.png)
* TargetClass.h TargetClass.m 追加&編集
* CoverageReportSampleTests.m 編集
* Project > CoverageReportSample > Generate Legacy Test Coverate Files > YES
![image](https://s3-ap-northeast-1.amazonaws.com/qiita/2/7605099f-6cb6-4ab1-b55a-55a8a33b684c.png)
* Project > CoverageReportSample > Instrument Program Flow > YES
![image](https://s3-ap-northeast-1.amazonaws.com/qiita/2/1ec03fb5-a79f-46cb-a6e2-fdf01377adff.png)
* TARGETS > Build Phases > + > New Run Script Phase > Pods/XcodeCoverage/exportenv.sh
![image](https://s3-ap-northeast-1.amazonaws.com/qiita/2/d44b5c3e-c327-4fdc-8c17-23a0fb9ca67e.png)
* pod init > PodfileにXcodeCoverage追加

##レポート生成手順
###1.Homebrewでlcovをインストール&パス確認

```
$ brew install lcov
==> Downloading https://homebrew.bintray.com/bottles/lcov-1.12.yosemite.bottle.tar.gz
Already downloaded: /Library/Caches/Homebrew/lcov-1.12.yosemite.bottle.tar.gz
==> Pouring lcov-1.12.yosemite.bottle.tar.gz
🍺  /usr/local/Cellar/lcov/1.12: 16 files, 533.3K

$ which lcov
/usr/local/bin/lcov

$ lcov --version
lcov: LCOV version 1.12
```

###2.pod install

```
$ cd {PROJECT_ROOT}
$ pod install
Updating local specs repositories

CocoaPods 1.0.0.beta.4 is available.
To update use: `gem install cocoapods --pre`
[!] This is a test version we'd love you to try.

For more information see http://blog.cocoapods.org
and the CHANGELOG for this version http://git.io/BaH8pQ.

Analyzing dependencies
Downloading dependencies
Installing XcodeCoverage (1.2.2)
Generating Pods project
Integrating client project
Sending stats
Pod installation complete! There is 1 dependency from the Podfile and 1 total pod installed.
```

###3.envcov.shの中身をbrewでインストールしたlcovのパスに書き換え
CocoaPodsに取得したXcodeCoverage内のenvcov.shに記載されているlcovの実行パスをHomebrewでインストールしたものに書き換えます。
この記事を書いている時点でのenvcov.shではXcodeCoverageに内蔵されているlcov-1.11で実行するように書かれていますがXcode7環境では上手く動作しませんでした([参考](http://stackoverflow.com/questions/32912030/xcode7-code-coverage-with-getcov-and-lcov))。

```
$ cd {PROJECT_ROOT}
$ vi Pods/XcodeCoverage/envcov.sh
8 - LCOV_PATH="${scripts}/lcov-1.11/bin"
8 + LCOV_PATH="/usr/local/bin/"
```

###4.テスト実行
CoverageReportSample.xcworkspaceを開きテストを実行します。
* CoverageReportSample.xcworkspaceを開く
* CoverageReportSample > 適当なエミュレーターを選択 > Product > Test

###5.XcodeCoverage実行
CocoaPodsに取得したXcodeCoverage内のgetcovを実行します。

```
$ cd {PROJECT_ROOT}
$ ./Pods/XcodeCoverage/getcov --show -o ~/Desktop/
Show HTML Report
output_dir = /Users/user/Desktop/
~/Desktop ~/Desktop/CoverageReportSample
~/Desktop/CoverageReportSample
Capturing coverage data from /Users/user/Library/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/Build/Intermediates/CoverageReportSample.build/Debug-iphonesimulator/CoverageReportSample.build/Objects-normal/x86_64
Found gcov version: 7.0.2
Found LLVM gcov version 3.4, which emulates gcov version 4.2
Scanning /Users/user/Library/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/Build/Intermediates/CoverageReportSample.build/Debug-iphonesimulator/CoverageReportSample.build/Objects-normal/x86_64 for .gcda files ...
Found 4 data files in /Users/user/Library/Developer/Xcode/DerivedData/CoverageReportSample-clwbjkiwcxqjnnaikakwgjmwcgtc/Build/Intermediates/CoverageReportSample.build/Debug-iphonesimulator/CoverageReportSample.build/Objects-normal/x86_64
Processing x86_64/AppDelegate.gcda
Processing x86_64/main.gcda
Processing x86_64/TargetClass.gcda
Processing x86_64/ViewController.gcda
Finished .info-file creation
Reading tracefile Coverage.info
Deleted 0 files
Writing data to Coverage.info
Summary coverage rate:
  lines......: 64.0% (16 of 25 lines)
  functions..: 60.0% (9 of 15 functions)
  branches...: no data found
Reading tracefile Coverage.info
Removing /Users/user/Desktop/CoverageReportSample/CoverageReportSample/main.m
Deleted 1 files
Writing data to Coverage.info
Summary coverage rate:
  lines......: 57.1% (12 of 21 lines)
  functions..: 57.1% (8 of 14 functions)
  branches...: no data found
Reading data file Coverage.info
Found 4 entries.
Found common filename prefix "/Users/user/Desktop/CoverageReportSample"
Writing .css and .png files.
Generating output.
Processing file CoverageReportSample/ViewController.m
Processing file CoverageReportSample/TargetClass.m
Processing file CoverageReportSample/AppDelegate.h
Processing file CoverageReportSample/AppDelegate.m
Writing directory view page.
Overall coverage rate:
  lines......: 57.1% (12 of 21 lines)
  functions..: 57.1% (8 of 14 functions)
```

##あとがき
結果はこんな感じにできあがります。
通っていない所は赤く表示され非常にわかりやすいですね！
![image](https://s3-ap-northeast-1.amazonaws.com/qiita/2/cadaef8a-9a4a-4aee-bc38-6550812ec837.png)

なお、Pod内で書き換えているenvcov.shは当然の事ながらPodが更新されると消える可能性があります。
自分は手間だったのでgnu-sedで置換するようにスクリプト作りました。

```
$ cd {PROJECT_ROOT}
$ touch coverage.sh
$ chmod +x coverage.sh
$ vi coverage.sh
#!/bin/bash

# brewでlcoveとgnu-sedをインストール
brew install lcove gnu-sed
# brew でのインストール先確認
# which lcov
# envcov.shのlcov参照先をbrewへ向ける
gsed -i '8c LCOV_PATH="/usr/local/bin/"' Pods/XcodeCoverage/envcov.sh
# カバレッジレポートをデスクトップへ出力
./Pods/XcodeCoverage/getcov --show -o ~/Desktop/
```