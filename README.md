based on https://github.com/nenoNaninu/NeuralVirtualCam
# NeuralVirtualCam
実際のカメラから取得した画像をGANで変換して仮想カメラ経由で垂れ流すやつ。
Linux or Windows GPU必須。

# Require
```
$ apt-get install v4l2loopback-utils

$ conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
$ conda install -c conda-forge opencv

$ pip install pyfakewebcam #for Linux
$ pip install pyvirtualcam #for Windows
```

- モデルのダウンロード
```
$ cd fast_neural_style 
$ python download_saved_models.py
```
# Usage
## 仮想カメラ

### for linux
```
$ ls /dev/|grep video
```
とかやると
```
video0
video1
video2
```
とか出てくる。今回video3を使っていないので、/dev/video3とかに流したいとする。その場合
```
$ sudo modprobe v4l2loopback video_nr=3
```
とコマンドを叩くことで仮想カメラの口をつくる。

### for windows
obs の仮想カメラをインストールするのみ

### os共通
口を用意したら
```
$ python main.py 接続先カメラ番号(default=0) 出力先パス(default=\dev\video3)
$ python main.py //defaultでいいなら省略可能

```



動画が表示されているウィンドウにフォーカスして操作
- q : 終了
- a,s,d,f : スタイル変更
- z : 無変換

# おまけ
web camに流れている映像を確認したい場合はffplayコマンドを使う（Linux）
```
ffplay /dev/video3
```

# こんな感じ。
LinuxのGPUマシン変換したものを仮想カメラ経由でGoogleハングアウトに垂れ流してMac book proで受信している。
![app](https://github.com/nenoNaninu/NeuralVirtualCam/blob/master/app.gif)

# ちなみに
Googleハングアウトにおいては、chromeには問題なく垂れ流せた。
FireFoxにおいてはさっくり動画を(普通のwebカメラでさえ)流せなかった...。
