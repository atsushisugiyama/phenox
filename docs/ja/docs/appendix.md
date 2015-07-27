<<<<<<< HEAD
#シリアル通信ソフトの設定方法## ホスト PC が Linux (Ubuntu12.10) の場合minicom を使って、シリアル通信を行います。必要に応じて、ホスト PC に minicom をインストー ルしてください。
```bash
sudo apt-get install minicom```
シリアル通信モジュール (FT232RL) とホスト PC を接続すると、`/dev/ttyUSB{+ 数字 }`, `/dev/ttyACM{+ 数字 }` などのデバイスファイルが現れますので、確認して下さい。その状態で、 minicom を起動します。

```bash
LANG=C sudo minicom -s
```

`Serial port setup` を選択します。
![Serial port setup] (/img/minicom1.png)

下図の通りに設定し、`Exit` を選択するとセットアップは完了です。この例では、シリアル通信モジュールが`/dev/ttyUSB0`として認識されています。
![Minicom Setting] (/img/minicom2.png)
=======
#シリアル通信ソフトの設定方法## ホスト PC が Linux (Ubuntu12.10) の場合minicom を使って、シリアル通信を行います。必要に応じて、ホスト PC に minicom をインストー ルしてください。```bashsudo apt-get install minicom```また、minicomの設定ファイルをダウンロードし、ホストPCに配置します。```bashwget http://phenoxlab.com/static/minirc.dflsudo mv minirc.dfl /etc/minicom/```シリアル通信モジュール (FT232RL) とホスト PC を接続すると、`/dev/ttyUSB{+ 数字 }`, `/dev/ttyACM{+ 数字 }` などのデバイスファイルが現れますので、確認して下さい。その状態で、 minicom を起動します。（Phenox2の電源を入れる必要はありません。）```bashsudo minicom ```以上で完了です。
>>>>>>> b3646279fc8e7a6d1b40b6e2a9286e07431ec70f
