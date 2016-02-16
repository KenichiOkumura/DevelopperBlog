#Cocoapods管理下のプロジェクトからStatic Libraryを作成する

Cocoapodsを利用しているプロジェクトをStatic Libraryとして出力する際の手法の小ネタです。  
結論から書くと[cocoapods-packager](https://github.com/CocoaPods/cocoapods-packager)を利用すれば一撃です。

Static Libraryを作成するにはxcodebuildを利用しRunScriptとかにスクリプト書いて実行するのがベターです。  
この辺りはググると山程出るのでそちらにお任せします。

今回はそんな中でCocoapodsを利用している場合です。  
Cocoapodsを利用していてもxcodebuildを使って出力することは可能でしたがもっと簡単な手法があったのでご紹介です。  
[cocoapods-packager](https://github.com/CocoaPods/cocoapods-packager)  
[podspec](https://guides.cocoapods.org/syntax/podspec.html)を記載する事でその内容をベースにStatic Libraryを作成してくれるライブラリです。
導入〜実行もpodspecファイルを作成し、gemで入れて追加されたpod packageを呼び出すだけ！
```
$ cd ${PROJECT_ROOT}
$ gem install cocoapods-packager
$ pod package Project.podspec
```
後は実行したディレクトリに作成されたproject.frameworkを利用するだけです。  
非常に簡単ですね。

ハマった点としてはpodspecファイルにspec.sourceの項目が記載されていないとrubyのエラーが表示されます。  
パット見rubyのバージョンとかの絡みか！？とか思ってしまい時間がかかりました…。  
ローカルのリポジトリしか無い場合でも下記な感じで記載すればOKでした。
```
spec.source = { :git => '/Users/sample/Project', :tag => 'develop' }
```

プロジェクト中でCocoapodsを利用し、参照している場合も良きに計らってくれました。  
皆様も是非お試しくださいませー