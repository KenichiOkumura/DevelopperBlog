https://blog.tagbangers.co.jp/ja/2016/12/02/switch_node_version

# nodeのバージョンを切り替えれるようにしたいです...。

nodeのバージョンを切り替えたい時はnodebrewを使うと便利です!(出オチ
[nodebrew](https://github.com/hokaccha/nodebrew)

Macで開発されてる方には馴染み深い [Homebrew](http://brew.sh/index_ja.html) のnode版です。※homebrew経由でnodebrewのインストールが可能です(brew install nodebrew)が、Yosemite以降は上手く動かないので公式にかかれている方法でインストールしてください。

セットアップ
```
~ $ curl -L git.io/nodebrew | perl - setup
~ $ echo "export PATH=$HOME/.nodebrew/current/bin:$PATH" >> .bash_profile
~ $ source .bash_profile
```

インストール
```
~ $ nodebrew install-binary stable
Fetching: https://nodejs.org/dist/v7.2.0/node-v7.2.0-darwin-x64.tar.gz
######################################################################## 100.0%
Installed successfully
~ $ nodebrew install-binary v7.0.0
Fetching: https://nodejs.org/dist/v7.0.0/node-v7.0.0-darwin-x64.tar.gz
######################################################################## 100.0%
Installed successfully
~ $ nodebrew use v7.0.0
use v7.0.0
~ $ node --version
v7.0.0
~ $ nodebrew use stable
use v7.2.0
~ $ node --version
v7.2.0
```