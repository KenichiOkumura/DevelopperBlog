https://blog.tagbangers.co.jp/ja/2015/02/05/chalenge_md-github

# 記事をMarkdownで書いてGitHubで公開してHTMLに変換して!

[https://github.com/KenichiOkumura/DevelopperBlog]
タイトルの通り先ほど投稿した[Mac環境でのAndroid楽々スクショ!](https://blog.tagbangers.co.jp/ja/2015/02/05/mac_for_ss)はMarkdown形式で記載したのをHTMLに変換してこのブログに乗っけてみました。
当ブログはWallrideという弊社独自のブログサービスなので記事を書く際にMarkdownには対応しておらず、[Redactor](http://imperavi.com/redactor/)というライブラリを利用してHTML形式にて記載しています。

ただせっかくエンジニアならMarkdownで記載するのが最近の流行ですよ!
ってことでやってみました。
やったことは下の感じです。

## Markdownエディターで記事を書く
[MacDown](http://macdown.uranusjr.com/)というツールを利用しました。
これ系のアプリは非常に沢山あるのですがイマイチしっくり来ませんでしたがこれは非常にシンプルで良いですね!

## 書いた記事をHTMLに変換する
MarkdownをHTML化してくれる物はたくさんあるんですがいかんせんクラスを付けてくれたりCSSを内包してくれたりしてコードの移植がしづらい。
色々探しましたが今回は[dillinger](http://dillinger.io/)というサイトを利用しました。
コードのシンタックスハイライト部分のcodeタグを除去することでそのまま移植が可能でした。
いつかmarkdown
for redactorとか作ってみたいですねぇ...。

## 書いた記事をGitHubに公開する
これは冒頭のリンクの通りGitHubに公開してみました。
Markdownでしっかり記載したのは初でしたが綺麗に見れて良いですね!
今後の記事もこの手法で公開していこうかと思います。
大したことはしてませんが今後は書いた記事のコードとかもGitHubで公開していけれたらなーとか考えてます。
記事に変更があった際はGitHubでStarしておくと通知来るので気になる方はすたーっちゃってくださいませ!