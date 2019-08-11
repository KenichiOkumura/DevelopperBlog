# AWS CodeDeployを試してみた

<div><p>
	Amazon Web Serviceより先日発表&amp;リリースされました CodeDeploy というサービスを試してみました。
</p><p>
	<strong><span data-redactor-tag="span" style="font-size: 18px;">CodeDeployとは</span></strong><span style="font-size: 18px;"></span>
</p><p style="margin-left: 20px;">
	<a href="http://aws.amazon.com/jp/codedeploy/">公式サイト</a>の文言を要約すると
</p><ul>
	<ul>
		<li>EC2インスタンスにコードを自動的に展開する</li>
		<li>展開する際のアプリケーションのダウンタイムを回避出来る</li>
		<li>複数台のEC2<span style="font-size: 14px;">インスタンスへの展開が簡単</span></li>
	</ul>
</ul><p style="margin-left: 20px;">
	っといった所が主たる機能だそうです。
</p><p>
	<strong><span data-redactor-tag="span" style="font-size: 18px;">CodeDeployを触ってみる</span></strong>
</p><p>
	<strong><span data-redactor-tag="span" style="font-size: 18px;"></span></strong>まずはサービス一覧からCodeDeployページに移動します。
</p><p>
	<img src="20141126_aws-code-deploy-trial/1.png">
</p><p>
	残念ながらTokyoリージョンではまだサービスが提供されていないのでバージニアへ移動します。
</p><p>
	<img src="20141126_aws-code-deploy-trial/2.png">
</p><p>
	CodeDeployのページが表示されました。
</p><p>
	早速「Get Started Now」へ!
</p><p>
	<img src="20141126_aws-code-deploy-trial/3.png">
</p><p>
	サンプルのコードか自分で指定したコードのどちらをデプロイするか聞かれます。
</p><p>
	今回は挙動を見るだけなので「Sample Deployment」を選択した状態で「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/4.png">
</p><p>
	次にデプロイするインスタンスの環境を指定します。
</p><p>
	「Key Pair Name」などは適当なものを作成&amp;指定します。
</p><p>
	現在は「Instance Type」はt1.microしか選べませんが将来的には増えたりしそうなので期待ですね。
</p><p>
	設定が問題なければ「Launch Instances」
</p><p>
	<img src="20141126_aws-code-deploy-trial/5.png">
</p><p>
	数秒後にCloudFormationへのリンクが表示されます。
</p><p>
	この時点で自動的にEC2インスタンスも立ち上がってます。
</p><p>
	特に変更点は無いのでそのまま「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/6.png">
</p><p>
	デプロイするアプリの名称を指定します。
</p><p>
	サンプルなんでそのままで「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/7.png">
</p><p>
	デプロイされるアプリの情報が表示されます。
</p><p>
	このページで実際にデプロイされるアプリのコードがダウンロードできます。
</p><p>
	特に設定項目はないのでそのまま「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/8.png">
</p><p>
	グループの名称設定とかができます。
</p><p>
	ここでEC2に振られるタグの名称とかも指定できるのでアプリによって変更するとわかりやすいですね。
</p><p>
	今回は全部そのままで「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/9.png">
</p><p>
	サービスロールの指定ができます。
</p><p>
	ロールに関してはこの時点で自動的に作成されていましたのでそのままの指定で「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/10.png">
</p><p>
	デプロイ設定画面です。
</p><p>
	「Default Deployment Configurations」ではAWS側から3種類のデプロイ方法が提供されています。
</p><p>
	それぞれ「1インスタンス毎にデプロイする」「半分のインスタンス毎にデプロイする」「全部まとめてデプロイする」の3パターンです。
</p><p>
	「Create Custom Deployment Configuration」を指定すると上記3種類以外にも自分で独自のデプロイ方法を作成することが可能です。
</p><p>
	今回はデフォルトで指定されてる「One at Time」のままで「Next Step」
</p><p>
	<img src="20141126_aws-code-deploy-trial/11.png">
</p><p>
	最後に今までの設定の確認です。
</p><p>
	問題など無ければそのまま「Deploy Now」!
</p><p>
	<img src="20141126_aws-code-deploy-trial/12.png">
</p><p>デプロイが開始されます。</p><p>
	しばらく待つとデプロイが完了します。
</p><p>
	<img src="20141126_aws-code-deploy-trial/13.png">
</p><p>
	<img src="20141126_aws-code-deploy-trial/14.png">
</p><p>
	<img src="20141126_aws-code-deploy-trial/15.png">
</p><p>
	この状態でEC2のインスタンスページへ行き、今回のデプロイで自動的に立ち上がったインスタンス3つのうち1つのPublic DNSへブラウザからアクセスすると無事サンプルページが表示されています。
</p><p>
	<img src="20141126_aws-code-deploy-trial/16.png">
</p><p>
	<img src="20141126_aws-code-deploy-trial/17.png">
</p><p>
	<br>
</p><p>
	これで無事にデプロイ完了です!
</p><p>
	<br>
</p><p>
	<span style="font-size: 18px;"><strong>所感とか</strong></span>
</p><p>
	<span style="font-size: 18px;"><span style="font-size: 14px;" data-redactor-style="font-size: 14px;">サンプルアプリなのもあってか思ったよりもさくさくと進めることができました。</span><em></em></span><span></span>
</p><p>
	思った以上に簡単だったので次は弊社プロダクトので試してみたいと思います。
</p><p>
	早くTokyoこいこい!
</p></div>