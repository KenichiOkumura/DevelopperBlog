#Mac環境でのAndroid楽々スクショ！

以前からAndroidでのスクリーンショットは結構手間がかかるものでした。  
実機があるならば本体のスクリーンショット機能を使ったりエミュレータならDeviceMonitorからスクショ撮ったりしてました。  
でもこれって結局実機に保存されたファイルを取り込まなくちゃだったりDeviceMonitorでも画面のリフレッシュを自動的にやってくれないのでまぁ面倒くさい。  
そこでなんかいい方法無いかなーと探してみたら下のコードに行き当たりました。  

```sh
adb shell screencap -p /sdcard/screen.png
adb pull /sdcard/screen.png
adb shell rm /sdcard/screen.png
```

超便利orz  
adbにそんな機能があったとは全く知らんかったです…。  
もっと早くググれば良かった…。  

って事でそんな便利なadbのスクリーンショット機能をデスクトップからサラッとシェルスクリプトを選択するだけで実行できるようにしてみました。  
下のコードは自分が使ってるコードになります。  
参照元では実行時直下に保存でしたがせっかくなんでデスクトップに保存してます。  
参照元：[adbでスクリーンショットを取るスクリプト](http://qiita.com/toshinarin/items/d0d1e9a36e88ea98bd72)  

```bash
$ touch ss.sh
$ chmod +x ./ss.sh
$ vi ./ss.sh
```

```bash:ss.sh
#!/bin/bash

DATE=`date +"%Y-%m-%d-%H-%M-%S"`
FILENAME="s-${DATE}.png"
echo "capturing ${FILENAME}..."
adb shell screencap -p "/sdcard/${FILENAME}"
adb pull /sdcard/"${FILENAME}" ./Desktop/"${FILENAME}"
adb shell rm "/sdcard/${FILENAME}"
echo "saved ${FILENAME}."
```

ついでにadbにpath通して無い人の為に通し方も乗っけておきます。  
私はあえて.bash_profileにパス系のはまとめて書いてます。  
~~.bash_profileはログイン時にロードされる場所なので下記記載後はPC再起動or再ログインが必要です。~~  
source .bash_profile でリロード出来るそうです…。  
便利ですね…。  

```bash
$ vi ./.bash_profile
$ source .bash_profile
```

```bash:.bash_profile
...

export ANDROID_HOME=/(AndroidSDKまでのパス)/android-sdks
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```