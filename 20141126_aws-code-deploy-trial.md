https://blog.tagbangers.co.jp/ja/2014/11/26/aws-code-deploy-trial

# AWS CodeDeployを試してみた
Amazon Web Serviceより先日発表&リリースされました CodeDeploy というサービスを試してみました。

## CodeDeployとは
[公式サイト](http://aws.amazon.com/jp/codedeploy/)の文言を要約すると
* EC2インスタンスにコードを自動的に展開する
* 展開する際のアプリケーションのダウンタイムを回避出来る
* 複数台のEC2インスタンスへの展開が簡単
っといった所が主たる機能だそうです。

## CodeDeployを触ってみる
まずはサービス一覧からCodeDeployページに移動します。
![1.png](20141126_aws-code-deploy-trial/1.png)
残念ながらTokyoリージョンではまだサービスが提供されていないのでバージニアへ移動します。
![2.png](20141126_aws-code-deploy-trial/2.png)
CodeDeployのページが表示されました。
早速「Get Started Now」へ!
![3.png](20141126_aws-code-deploy-trial/3.png)
サンプルのコードか自分で指定したコードのどちらをデプロイするか聞かれます。
今回は挙動を見るだけなので「Sample Deployment」を選択した状態で「Next Step」
![4.png](20141126_aws-code-deploy-trial/4.png)
次にデプロイするインスタンスの環境を指定します。
「Key Pair Name」などは適当なものを作成&指定します。
現在は「Instance Type」はt1.microしか選べませんが将来的には増えたりしそうなので期待ですね。
設定が問題なければ「Launch Instances」
![5.png](20141126_aws-code-deploy-trial/5.png)
数秒後にCloudFormationへのリンクが表示されます。
この時点で自動的にEC2インスタンスも立ち上がってます。
特に変更点は無いのでそのまま「Next Step」
![6.png](20141126_aws-code-deploy-trial/6.png)
デプロイするアプリの名称を指定します。
サンプルなんでそのままで「Next Step」
![7.png](20141126_aws-code-deploy-trial/7.png)
デプロイされるアプリの情報が表示されます。
このページで実際にデプロイされるアプリのコードがダウンロードできます。
特に設定項目はないのでそのまま「Next Step」
![8.png](20141126_aws-code-deploy-trial/8.png)
グループの名称設定とかができます。
ここでEC2に振られるタグの名称とかも指定できるのでアプリによって変更するとわかりやすいですね。
今回は全部そのままで「Next Step」
![9.png](20141126_aws-code-deploy-trial/9.png)
サービスロールの指定ができます。
ロールに関してはこの時点で自動的に作成されていましたのでそのままの指定で「Next Step」
![10.png](20141126_aws-code-deploy-trial/10.png)
デプロイ設定画面です。
「Default Deployment Configurations」ではAWS側から3種類のデプロイ方法が提供されています。
それぞれ「1インスタンス毎にデプロイする」「半分のインスタンス毎にデプロイする」「全部まとめてデプロイする」の3パターンです。
「Create Custom Deployment Configuration」を指定すると上記3種類以外にも自分で独自のデプロイ方法を作成することが可能です。
今回はデフォルトで指定されてる「One at Time」のままで「Next Step」
![11.png](20141126_aws-code-deploy-trial/11.png)
最後に今までの設定の確認です。
問題など無ければそのまま「Deploy Now」!
![12.png](20141126_aws-code-deploy-trial/12.png)
しばらく待つとデプロイが完了します。
![13.png](20141126_aws-code-deploy-trial/13.png)
![14.png](20141126_aws-code-deploy-trial/14.png)
![15.png](20141126_aws-code-deploy-trial/15.png)
この状態でEC2のインスタンスページへ行き、今回のデプロイで自動的に立ち上がったインスタンス3つのうち1つのPublic DNSへブラウザからアクセスすると無事サンプルページが表示されています。
![16.png](20141126_aws-code-deploy-trial/16.png)
![17.png](20141126_aws-code-deploy-trial/17.png)

これで無事にデプロイ完了です!

---

## 所感とか
サンプルアプリなのもあってか思ったよりもさくさくと進めることができました。
思った以上に簡単だったので次は弊社プロダクトので試してみたいと思います。
早くTokyoこいこい!