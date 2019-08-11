# OSXでHomebrewでAWS CLIをTabComplation

<div><p>ほぼタイトルそのままです。<br>OSXにHomebrewを使ってAWS CLIをインストールし、Tab押した際の保管機能を効かせる方法です。<br>通常のインストールだとcliで利用できるコマンドがTabで保管されず、不便だなーと思ったので調べてみました。<br>調べてみると<a href="https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-command-completion.html#cli-command-completion-enable" target="_blank">公式</a>にしっかりと書いてありました。<br>ドキュメントは大事ですね。</p><pre class="bash hljs">~ $ brew install awscli
==&gt; Downloading <a class="vglnk" href="https://homebrew.bintray.com/bottles/awscli-" rel="nofollow"><span>https</span><span>://</span><span>homebrew</span><span>.</span><span>bintray</span><span>.</span><span>com</span><span>/</span><span>bottles</span><span>/</span><span>awscli</span><span>-</span></a><span class="hljs-number">1.11</span>.<span class="hljs-number">23</span>.sierra.bottle.tar.gz
<span class="hljs-comment">######################################################################## 100.0%</span>
==&gt; Pouring awscli-<span class="hljs-number">1.11</span>.<span class="hljs-number">23</span>.sierra.bottle.tar.gz
==&gt; Caveats
The <span class="hljs-string">"examples"</span> directory has been installed to:
&nbsp; /usr/<span class="hljs-built_in">local</span>/share/awscli/examples

Before using aws-cli, you need to tell it about your AWS credentials.
The quickest way to <span class="hljs-keyword">do</span> this is to run:
&nbsp; aws configure

More information:
&nbsp; <a class="vglnk" href="https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html" rel="nofollow"><span>https</span><span>://</span><span>docs</span><span>.</span><span>aws</span><span>.</span><span>amazon</span><span>.</span><span>com</span><span>/</span><span>cli</span><span>/</span><span>latest</span><span>/</span><span>userguide</span><span>/</span><span>cli</span><span>-</span><span>chap</span><span>-</span><span>getting</span><span>-</span><span>started</span><span>.</span><span>html</span></a>
&nbsp; <a class="vglnk" href="https://pypi.python.org/pypi/awscli" rel="nofollow"><span>https</span><span>://</span><span>pypi</span><span>.</span><span>python</span><span>.</span><span>org</span><span>/</span><span>pypi</span><span>/</span><span>awscli</span></a><span class="hljs-comment">#getting-started</span>

Bash completion has been installed to:
&nbsp; /usr/<span class="hljs-built_in">local</span>/etc/bash_completion.d

zsh completion has been installed to:
&nbsp; /usr/<span class="hljs-built_in">local</span>/share/zsh/site-functions
==&gt; Summary
&nbsp; /usr/<span class="hljs-built_in">local</span>/Cellar/awscli/<span class="hljs-number">1.11</span>.<span class="hljs-number">23</span>: <span class="hljs-number">3</span>,<span class="hljs-number">510</span> files, <span class="hljs-number">29.3</span>M

~ $ complete -C <span class="hljs-string">'/usr/local/bin/aws_completer'</span> aws
</pre></div>