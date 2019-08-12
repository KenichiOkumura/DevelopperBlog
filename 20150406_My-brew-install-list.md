https://blog.tagbangers.co.jp/ja/2015/04/06/My-brew-install-list

# My brew install list
続編書きました
[My set up list to 2016](https://blog.tagbangers.co.jp/ja/2016/08/31/My_set_up_list_to_2016)

---

タイトルの英語は適当です。
Macにはcentosとかのyumやubuntuのapt-get的なHomebrewというツールがあります。
こちらパッと見あんまり使わないんじゃねぇの...?的なイメージを受けるかもしれませんがPCセットアップ直後の開発環境セットアップの際にそのパワーを発揮します。
今回はHomebrew自体の説明は省いて私が個人的にPCセットアップ後に流してるbrewの対象を公開いたします。
弊社の開発部隊(Mac利用者)では大体これぐらいあれば事足ります。

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install git
brew install wget
brew install boot2docker
brew installqprint
brew install imagemagick
brew install maven
brew tap caskroom/cask
brew install mysql
brew install postgresql
brew cask install appcode
brew cask install android-studio
brew cask install intellij-idea
brew cask install google-japanese-ime
brew cask install sublime-text3
brew cask install google-chrome
brew cask install firefox-ja
brew cask install sourcetree
brew cask install evernote
brew cask install dropbox
brew cask install virtualbox
brew cask install genymotion
brew cask install sequel-pro
brew cask install pg-commander
brew cask install pgadmin3
brew cask install mysqlworkbench
```