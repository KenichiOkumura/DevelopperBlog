https://blog.tagbangers.co.jp/ja/

# My set up list to 2016

<div><p>以前書いた<a href="https://blog.tagbangers.co.jp/ja/2015/04/06/My-brew-install-list" target="_blank">記事</a>が社内でMacユーザーのデフォページ化してきましたが流石に書いてから1年も経つ物をそのままなのはどうかなーと思ったのでメンテナンスを兼ねて2016年版書きます。<br>ただ書き換えるだけも何なので前回から<br></p><ul><li>初期セットアップする際に自分が変更してる項目</li><li>brewでインストールする物を見直し</li><li>オススメGUIツール</li></ul><p>を追加しました。</p><p><br></p><p>Homebrewとは → <a href="http://brew.sh/index_ja.html" target="_blank">http://brew.sh/index_ja.html</a></p><h3>OSX 設定項目</h3><h4>設定 &gt; デスクトップとスクリーンセーバー</h4><p><input type="checkbox">&nbsp;開始までの時間 : 5分<br></p><h4>設定 &gt; Dock</h4><p><input type="checkbox">&nbsp;Dock を自動的に隠す / 表示 : ☑<br></p><h4>設定 &gt; Missing Control</h4><p><input type="checkbox">&nbsp;アプリケーションの切り替えで、アプリケーションのウインドウが開いている操作スペースに移動 : ☑<br><input type="checkbox">&nbsp;ウインドウをアプリケーションごとにグループ化 : ☐<br><input type="checkbox">&nbsp;ディスプレイ毎に個別の操作スペース : ☑<br></p><h4>設定 &gt; セキュリティとプライバシー &gt; 一般</h4><p><input type="checkbox">&nbsp;スリープとスクリーンセーバの解除にパスワードを要求 開始後 : 5秒後に : ☑<br></p><h4>設定 &gt; キーボード &gt; キーボード</h4><p><input type="checkbox">&nbsp;キーのリピート : 早い<br><input type="checkbox">&nbsp;リピート入力認識までの時間 : 短い<br><input type="checkbox">&nbsp;F1、F2などの全てのキーを標準のファンクションキーとして使用 : ☑<br></p><h4>設定 &gt; キーボード &gt; キーボード &gt; 修飾キー</h4><p><input type="checkbox">&nbsp;Caps Lock(⇪) : ⌘ Command<br></p><h4>設定 &gt; キーボード &gt; ショートカット &gt; Spotlight</h4><p><input type="checkbox">&nbsp;Spotlight検索を表示 : ☐<br><input type="checkbox">&nbsp;Finderの検索ウインドウを表示 : ☐<br></p><h4>設定 &gt; マウス</h4><p><input type="checkbox">&nbsp;スクロールの方向 : ナチュラル : ☑<br></p><h4>設定 &gt; トラックパッド &gt; ポイントとクリック</h4><p><input type="checkbox">&nbsp;タップでクリック : ☑<br><input type="checkbox">&nbsp;副ボタンのクリック : ☑<br><input type="checkbox">&nbsp;副ボタンのクリック : 2本指でクリックまたはタップ<br><input type="checkbox">&nbsp;調べる : ☐<br><input type="checkbox">&nbsp;3本指のドラッグ : ☑<br><input type="checkbox">&nbsp;軌跡の速さ : 速い<br></p><h4>設定 &gt; トラックパッド &gt; スクロールとズーム</h4><p><input type="checkbox">&nbsp;スクロールの方向 : ナチュラル : ☐<br><input type="checkbox">&nbsp;拡大/縮小 : ☑<br></p><h4>設定 &gt; トラックパッド &gt; その他のジェスチャ</h4><p><input type="checkbox">&nbsp;ページ間をスワイプ : 2本指で左右にスクロール : ☑<br><input type="checkbox">&nbsp;通知センター : ☐<br><input type="checkbox">&nbsp;Missing Control : 4本指で上にスワイプ : ☑<br><input type="checkbox">&nbsp;アプリケーション Expose : 4本指で下にスワイプ : ☑<br><input type="checkbox">&nbsp;Launchpad : ☑<br><input type="checkbox">&nbsp;デスクトップを表示 : ☑<br></p><h4>設定 &gt; アクセシビリティ &gt; ズーム機能</h4><p><input type="checkbox">&nbsp;スクロールジェスチャと修飾キーを使ってズーム : ^ Control : ☑<br></p><h3>ターミナル</h3><pre class="bash hljs"><span class="hljs-comment"># /User/{name}/ へ移動</span>
<span class="hljs-built_in">cd</span> ~

<span class="hljs-comment"># Homebrewのインストール</span>
ruby <span class="hljs-operator">-e</span> <span class="hljs-string">"<span class="hljs-variable">$(curl -fsSL <a class="vglnk" href="https://raw.githubusercontent.com/Homebrew/install/master/install" rel="nofollow"><span>https</span><span>://</span><span>raw</span><span>.</span><span>githubusercontent</span><span>.</span><span>com</span><span>/</span><span>Homebrew</span><span>/</span><span>install</span><span>/</span><span>master</span><span>/</span><span>install</span></a>)</span>"</span>

<span class="hljs-comment"># Java開発</span>
brew install brew-cask
brew tap caskroom/cask
brew tap caskroom/versions
brew cask install java6
brew cask install java7
brew cask install java8
<span class="hljs-built_in">echo</span> <span class="hljs-string">"export JAVA_HOME=\$(/usr/libexec/java_home -v 1.8)"</span> &gt;&gt; .bash_profile
<span class="hljs-built_in">source</span> .bash_profile

<span class="hljs-comment"># 開発必須系</span>
brew install git
brew install wget
brew install jq
brew install pv
brew install awscli
brew install gradle
brew install maven
brew install node
brew install imagemagick

<span class="hljs-comment"># GNU系とdateコマンドを揃える</span>
<span class="hljs-comment"># <a class="vglnk" href="http://qiita.com/dongri/items/7b142c138e650785bd72" rel="nofollow"><span>http</span><span>://</span><span>qiita</span><span>.</span><span>com</span><span>/</span><span>dongri</span><span>/</span><span>items</span><span>/</span><span>7b142c138e650785bd72</span></a></span>
brew install coreutils
<span class="hljs-built_in">echo</span> <span class="hljs-string">"alias date=\"gdate\""</span> &gt;&gt; .bashrc
<span class="hljs-built_in">source</span> .bashrc

<span class="hljs-comment"># DB</span>
brew install mysql
brew install postgresql

<span class="hljs-comment"># iOS開発</span>
sudo gem install cocoapods
brew install appledoc
brew install lcov

<span class="hljs-comment"># Android開発</span>
brew install android-sdk

<span class="hljs-comment"># おまけ</span>

<span class="hljs-comment"># <a class="vglnk" href="http://qiita.com/suin/items/bc3fe53b3630a40e045b" rel="nofollow"><span>http</span><span>://</span><span>qiita</span><span>.</span><span>com</span><span>/</span><span>suin</span><span>/</span><span>items</span><span>/</span><span>bc3fe53b3630a40e045b</span></a></span>
brew install figlet

<span class="hljs-comment"># ターミナルの$以前を簡略化</span>
<span class="hljs-built_in">echo</span> <span class="hljs-string">"export PS1='\\W \$ '"</span> &gt;&gt; .bash_profile
</pre><h3>GUIツール</h3><h4>IDE</h4><ul><li><a href="https://www.jetbrains.com/idea/" target="_blank">IntelliJ IDEA</a></li><li><a href="https://developer.android.com/studio/index.html?hl=ja" target="_blank">Android Studio</a></li><li><a href="https://itunes.apple.com/jp/app/xcode/id497799835?mt=12" target="_blank">Xcode</a></li><li><a href="https://www.jetbrains.com/objc/" target="_blank">AppCode</a></li></ul><h4>テキストエディタ(メモ帳)</h4><ul><li><a href="https://www.sublimetext.com/3" target="_blank">Sublime Text 3</a></li><li><a href="https://atom.io/" target="_blank">ATOM</a></li><li><a href="https://www.mimikaki.net/" target="_blank">mi</a></li></ul><h4>テキストエディタ(md)</h4><ul><li><a href="http://macdown.uranusjr.com/" target="_blank">MacDown</a></li><li><a href="http://kobito.qiita.com/" target="_blank">Kobito</a></li></ul><h4>ファイル転送</h4><ul><li><a href="https://panic.com/jp/transmit/" target="_blank">Transmit</a></li><li><a href="https://cyberduck.io/index.ja.html?l=ja" target="_blank">Cyberduck</a></li><li><a href="https://filezilla-project.org/" target="_blank">FileZilla</a></li></ul><h4>Git</h4><ul><li><a href="https://ja.atlassian.com/software/sourcetree" target="_blank">SourceTree</a></li><li><a href="https://www.gitkraken.com/" target="_blank">GitKraken</a></li></ul><h4>ブラウザ</h4><ul><li><a href="https://www.google.co.jp/chrome/browser/desktop/" target="_blank">Google Chrome</a></li><li><a href="https://www.google.co.jp/chrome/browser/canary.html" target="_blank">Google Chrome Canary</a></li><li><a href="https://www.mozilla.org/ja/firefox/new/" target="_blank">Firefox</a></li><li><a href="https://www.mozilla.org/ja/firefox/developer/" target="_blank">Firefox Developer Edition</a></li></ul><h4>Chrome Extension</h4><ul><li><a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop" target="_blank">Postman(アプリ版)</a></li><li><a href="https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm" target="_blank">Postman(タブ版)</a></li><li><a href="https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo" target="_blank">Postman Interceptor</a></li><li><a href="https://chrome.google.com/webstore/detail/user-agent-switcher-for-c/djflhoibgkdhkhhcedjiklpkjnoahfmg" target="_blank">User-Agent Switcher</a></li><li><a href="https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc" target="_blank">JSONView</a></li><li><a href="https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei" target="_blank">LiveReload</a></li><li><a href="https://chrome.google.com/webstore/detail/screencastify-screen-vide/mmeijimgabbpbgpdklnllpncmdofkcpn" target="_blank">Screencastify</a></li></ul><h4>DBブラウザ</h4><h6>共通最強</h6><ul><li><a href="https://www.jetbrains.com/datagrip/" target="_blank">DataGrip</a></li><li><a href="https://www.jetbrains.com/help/idea/2016.2/database-tool-window.html" target="_blank">IntelliJ IDEA Database Tool window</a></li></ul><h6>MySQL</h6><ul><li><a href="http://www.sequelpro.com/" target="_blank">Sequel Pro</a></li><li><a href="https://www-jp.mysql.com/products/workbench/" target="_blank">MySQL Workbench</a></li></ul><h6>PostgreSQL</h6><ul><li><a href="https://eggerapps.at/postico/" target="_blank">Postico</a></li><li><a href="https://www.pgadmin.org/" target="_blank">pgAdmin3</a></li></ul><h6>SQLite</h6><ul><li><a href="http://datumapps.com/datum.html" target="_blank">Datum</a></li></ul><h6>ORACLE</h6><ul><li><a href="http://www.oracle.com/technetwork/jp/developer-tools/sql-developer/overview/index.html" target="_blank">SQL Developer</a></li></ul><h4>IME</h4><ul><li><a href="https://www.google.co.jp/ime/" target="_blank">Google 日本語入力</a></li></ul><h4>PDF Viewr</h4><ul><li><a href="http://skim-app.sourceforge.net/" target="_blank">Skim</a></li></ul><h4>その他オススメ</h4><h6>メモリークリーナー</h6><ul><li><a href="https://fiplab.com/apps/memory-clean-for-mac" target="_blank">Memory Clean</a></li></ul><h6>カラーピッカー</h6><ul><li><a href="http://sipapp.io/" target="_blank">Sip</a></li></ul><h6>右上メニュー整理</h6><ul><li><a href="https://www.macbartender.com/" target="_blank">Bartender</a></li></ul><h6>ウィンドウ配置</h6><ul><li><a href="http://magnet.crowdcafe.com/" target="_blank">Magnet</a></li></ul><h6>SVG Viewr, Export</h6><ul><li><a href="http://gapplin.wolfrosch.com/" target="_blank">Gapplin</a></li></ul><h6>Zip Utility</h6><ul><li><a href="http://unarchiver.c3.cx/unarchiver" target="_blank">The Unarchiver</a></li><li><a href="http://ynomura.com/home/?page_id=116" target="_blank">MacZip4Win</a></li></ul><h6>Image Editor</h6><ul><li><a href="https://www.sketchapp.com/" target="_blank">Sketch</a></li><li><a href="http://www.pixelmator.com/mac/" target="_blank">Pixelmator</a></li><li><a href="https://evernote.com/intl/jp/skitch/" target="_blank">Skitch</a></li></ul></div>