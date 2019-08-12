https://blog.tagbangers.co.jp/ja/2016/12/02/osx_homebrew_awscli_tab

# OSXでHomebrewでAWS CLIをTabComplation

ほぼタイトルそのままです。
OSXにHomebrewを使ってAWS CLIをインストールし、Tab押した際の保管機能を効かせる方法です。
通常のインストールだとcliで利用できるコマンドがTabで保管されず、不便だなーと思ったので調べてみました。
調べてみると[公式](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-command-completion.html#cli-command-completion-enable)にしっかりと書いてありました。
ドキュメントは大事ですね。

```
~ $ brew install awscli
==> Downloading https://homebrew.bintray.com/bottles/awscli-1.11.23.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring awscli-1.11.23.sierra.bottle.tar.gz
==> Caveats
The "examples" directory has been installed to:
  /usr/local/share/awscli/examples

Before using aws-cli, you need to tell it about your AWS credentials.
The quickest way to do this is to run:
  aws configure

More information:
  https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html
  https://pypi.python.org/pypi/awscli#getting-started

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d

zsh completion has been installed to:
  /usr/local/share/zsh/site-functions
==> Summary
  /usr/local/Cellar/awscli/1.11.23: 3,510 files, 29.3M

~ $ complete -C '/usr/local/bin/aws_completer' aws
```