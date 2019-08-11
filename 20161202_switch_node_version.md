# nodeのバージョンを切り替えれるようにしたいです...。

<div><p>nodeのバージョンを切り替えたい時はnodebrewを使うと便利です!(出オチ</p><h2><a href="https://github.com/hokaccha/nodebrew" target="_blank">nodebrew</a></h2><p>Macで開発されてる方には馴染み深い<a href="http://brew.sh/index_ja.html" target="_blank">Homebrew</a>のnode版です。<br>※homebrew経由でnodebrewのインストールが可能です(brew install nodebrew)が、Yosemite以降は上手く動かないので公式にかかれている方法でインストールしてください。</p><p>セットアップ</p><pre class="bash hljs">~ $ curl -L <a class="vglnk" href="http://git.io/nodebrew" rel="nofollow"><span>git</span><span>.</span><span>io</span><span>/</span><span>nodebrew</span></a> | perl - setup
~ $ <span class="hljs-built_in">echo</span> <span class="hljs-string">"export PATH=<span class="hljs-variable">$HOME</span>/.nodebrew/current/bin:<span class="hljs-variable">$PATH</span>"</span> &gt;&gt; .bash_profile
~ $ <span class="hljs-built_in">source</span> .bash_profile
</pre><p>インストール</p><pre class="bash hljs">~ $ nodebrew install-binary stable
Fetching: <a class="vglnk" href="https://nodejs.org/dist/v7" rel="nofollow"><span>https</span><span>://</span><span>nodejs</span><span>.</span><span>org</span><span>/</span><span>dist</span><span>/</span><span>v7</span></a>.<span class="hljs-number">2.0</span>/node-v7.<span class="hljs-number">2.0</span>-darwin-x64.tar.gz
<span class="hljs-comment">######################################################################## 100.0%</span>
Installed successfully
~ $ nodebrew install-binary v7.<span class="hljs-number">0.0</span>
Fetching: <a class="vglnk" href="https://nodejs.org/dist/v7" rel="nofollow"><span>https</span><span>://</span><span>nodejs</span><span>.</span><span>org</span><span>/</span><span>dist</span><span>/</span><span>v7</span></a>.<span class="hljs-number">0.0</span>/node-v7.<span class="hljs-number">0.0</span>-darwin-x64.tar.gz
<span class="hljs-comment">######################################################################## 100.0%</span>
Installed successfully
~ $ nodebrew use v7.<span class="hljs-number">0.0</span>
use v7.<span class="hljs-number">0.0</span>
~ $ node --version
v7.<span class="hljs-number">0.0</span>
~ $ nodebrew use stable
use v7.<span class="hljs-number">2.0</span>
~ $ node --version
v7.<span class="hljs-number">2.0</span>
</pre></div>