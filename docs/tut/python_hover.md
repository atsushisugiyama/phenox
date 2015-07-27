このチュートリアルは以下の作業の習得を目的としています。なお、ホストPCとしてUbuntu14.04を使用します。

- サンプルコードを実行し、PythonコードでPhenoxを飛行させるための基本的な方法を例示します。
- PythonコードでPhenoxを飛行させる際、安全上注意すべき点を確認します。

本チュートリアルの前に[Python環境の構築](../dev/pythonenv)および[Pythonでのプログラム実行](./python_led)を完了していることが前提となっています。また飛行に際しては以下のことに注意してください。

 - 屋内環境下で 3m x 3m 以上の、平坦な地面をしたスペースを用意してくでさい。
 - 絨毯などの柔らかい素材よりも、コンクリートなどの固い素材の方が、高度方向の制御が安定します。
 - 空調などの風が起こる装置はあらかじめ切っておきます。


# 1. サンプルコードの入手と配置
サンプルコードの入手と配置は[Pythonでのプログラム実行](./python_led)で完了しているため、本チュートリアルでは特に必要ありません。

# 2. Phenox2 へログイン
[プロジェクトのビルド](./build)を参考に、Phenox2にsshで`root`としてログインしてください。

# 3. プログラムの実行: 状態量の確認
このプログラムは以下の動作を行います。

1. Phenoxライブラリの初期化
2. ユーザーによって笛が鳴らされるまで待機
3. 笛の音に反応して離陸
4. ホバー状態に入り、その場静止をするように飛行制御

まず待機状態のPhenoxの各種状態量を確認してみましょう。以下のコマンドでプログラムを実行します。

```bash
cd /root/phenox/work/tutorial_python
python ./autohover.py
```

プログラム開始時にはPhenox2がジャイロセンサーなどの初期化を行うので、必ずPhenox2を安定した場所で静止させて、手に持つことはしないで下さい。開始から3秒程で初期化は完了し、 `CPU0:Finished Initialization.` というメッセージが現れます。

初期化が完了すると状態量が表示されます。状態量の数字は、それぞれ `px_selfstate` 構造体のメンバー変数 (`degx`, `degy`, `degz`, `vision_tx`, `vision_ty`, `vision_tz`, `height`)を表しています。状態量の表示が開始されたら、Phenox2 を持ち上げて、動かし、各状態量が変化することを確認してみてください。また本チュートリアルでは確認できませんが、C言語版チュートリアルである[Phenoxの飛行](controll)で触れられているように、地面上に特徴点があることが安定した飛行の条件となるため、床面の環境を確認してください。


# 4. プログラムの実行: 飛行
地面の環境整備が完了したら、Phenox2を地面の上に置き、Phenox2の近くで笛を大きく吹いてください。離陸が始まります。笛の音を検出すると3秒間のスタートアップ状態の後、上昇 (`PX_UP`) し、ホバー状態 (`PX_HOVER`) となり, 高度方向、水平方向に状態を保つように飛行制御が行われます。ホバー状態から笛の音を再び検出するか、Phenox2の足を掴んで大きく傾けることで、Phenox2の飛行を止めることができます。
