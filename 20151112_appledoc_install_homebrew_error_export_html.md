# AppleDocをHomebrewでインストールした際にHTMLが出力されない

<p>AppledocとはいわゆるObjective-C版のJavadocでAppleのドキュメントと同じようなスタイルで出力してくれる大変便利なツールです。
    <br><a href="https://github.com/tomaz/appledoc">https://github.com/tomaz/appledoc</a></p>
<p>これを使ってHTMLを出力してみようと下記コマンドを実行してみる</p><pre>$ appledoc -p sample --project-company Tagbangers --create-html --no-create-docset --output ./docs/ ./</pre>
<p>出ない...?</p>
<p>そ、そんな馬鹿な!?
    <br>そうか!company-idが指定してないからだ!</p><pre>$ appledoc -p sample --project-company Tagbangers --create-html --no-create-docset --company-id jp.co.tagbangers.sample --output ./docs/ ./</pre>
<p>で、出ない...??
    <br>出力はされるのに中身が空っぽの状態で出力されてしまいました...。</p>
<p>何故だ...何が悪いんだ...。
    <br>とりあえずログと設定出してみるか...。</p><pre>$ appledoc -p sample --project-company Tagbangers --create-html --no-create-docset --company-id jp.co.tagbangers.sample --print-setting --verbose 4 --output ./docs/ ./
Settings used for this run:
--project-name = sample
--project-version = 1.0
--project-company = Tagbangers
--company-id = jp.co.tagbangers.aescrypt
--templates = /usr/local/Cellar/appledoc/2.2.1/Templates
--output = /code/sample/docs
...
INFO | Generating output for hierarchy...
INFO | Finished generating in 35ms.
NORMAL | Finished in 75ms.
INFO | Parsing:    37ms (49%)
INFO | Processing: 3ms (4%)
INFO | Generating: 35ms (46%)</pre>
<p>別に問題なさそうだな...。
    <br>まず出力されたHTMLファイルにCSS入ってないし...。
    <br>
    <br>
    <br>
    <br>
    <br>あれ?これテンプレート怪しくね...?</p><pre>$ ls -all /usr/local/Cellar/appledoc/2.2.1/Templates/html/css/
total 16
drwxr-xr-x@  4 sample  admin   136 11  6 11:51 .
drwxr-xr-x@  9 sample  admin   306 11  6 11:51 ..
drwxr-xr-x@ 10 sample  admin   340 11  6 11:51 scss</pre>
<p>やっぱstyle.cssとか無いな...?でもGithubのコードにはある...?
    <br>...これかな...?w</p><pre>$ mv /usr/local/Cellar/appledoc/2.2.1/Templates/ /usr/local/Cellar/appledoc/2.2.1/_Templates/
$ wget https://github.com/tomaz/appledoc/archive/master.zip
$ unzip master.zip
$ mv ./appledoc-master/Templates/ /usr/local/Cellar/appledoc/2.2.1/Templates/
$ appledoc -p sample --project-company Tagbangers --create-html --no-create-docset --company-id jp.co.tagbangers.sample --print-setting --verbose 4 --output ./docs/ ./</pre>
<p>出力されましたorz
    <br>っということで現時点(2015/11/12)で最新の2.2.1をHomebrew経由でインストールした方はGithubから元ソース落としてTemplateフォルダを上書き若しくはダウンロードしたフォルダを--templatesパラメータで指定してあげると出力できます!</p>
