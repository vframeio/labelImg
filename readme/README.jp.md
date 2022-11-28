---
title: labelImg
---

[![image](https://img.shields.io/pypi/v/labelimg.svg)](https://pypi.python.org/pypi/labelimg)

![image](https://img.shields.io/github/workflow/status/tzutalin/labelImg/Package?style=for-the-badge%20%20%20:alt:%20GitHub%20Workflow%20Status)

[![image](https://img.shields.io/badge/lang-en-blue.svg)](https://github.com/tzutalin/labelImg)

[![image](https://img.shields.io/badge/lang-zh-green.svg)](https://github.com/tzutalin/labelImg/blob/master/readme/README.zh.md)

[![image](https://img.shields.io/badge/lang-jp-green.svg)](https://github.com/tzutalin/labelImg/blob/master/readme/README.jp.md)

![image](/resources/icons/app.png){.align-center width="200px"}

LabelImgは、PythonとQtを使うアノテーション補助ツールです。

このツールはPascalVOCフォーマットとYOLOとCreateMLをサポートしています。

![Demo Image](../demo/demo3.jpg)

![Demo Image](../demo/demo.jpg)

[サンプル動画は
\<https://youtu.be/p0nR2YsCY\_U\>にあります。]{.title-ref}\_\_

インストール方法
================

ソースからビルドする
--------------------

Linuxまたは、Ubuntuまたは、macOSの場合は

### Ubuntuの場合

Python 3とQt5を使う場合

``` {.shell}
sudo apt-get install pyqt5-dev-tools
sudo pip3 install -r requirements/requirements-linux-python3.txt
make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

### macOSの場合

Python 3とQt5を使う場合

``` {.shell}
brew install qt  # Install qt-5.x.x by Homebrew
brew install libxml2

or using pip

pip3 install pyqt5 lxml # Install qt and lxml by pip

make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 Virtualenv (推奨)

VirtualenvはQtとPythonのバージョン衝突問題を解消できます。

``` {.shell}
brew install python3
pip3 install pipenv
pipenv run pip install pyqt5==5.15.2 lxml
pipenv run make qt5py3
pipenv run python3 labelImg.py
[任意で] rm -rf build dist; python setup.py py2app -A;mv "dist/labelImg.app" /Applications
```

注意：最後のコマンドを実行すると、/ApplicationsフォルダにSVGアイコンを含む.appファイルが生成されます。build-tools/build-for-macos.shというスクリプトの仕様も検討してください。

### Windowsの場合

最初に[Python](https://www.python.org/downloads/windows/) と
[PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5) と
[install lxml](http://lxml.de/installation.html)
をインストールしてください。

コマンドプロンプトを起動し [labelImg](#labelimg)
がインストールされているフォルダに移動してから以下のコマンドを実行します。

``` {.shell}
pyrcc4 -o libs/resources.py resources.qrc
（pyqt5の場合は、 pyrcc5 -o libs/resources.py resources.qrc）

python labelImg.py
python labelImg.py [画像パス] [定義済みクラスファイル]
```

### Windows + Anaconda

[Anaconda](https://www.anaconda.com/download/#download)
をダウンロードしてからインストールしてください。

Anaconda Promptを起動し [labelImg](#labelimg)
インストールされているフォルダに移動してから以下のコマンドを実行します。

``` {.shell}
conda install pyqt=5
conda install -c anaconda lxml
pyrcc5 -o libs/resources.py resources.qrc
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

PyPIから入手する（Python 3以降のみ）
------------------------------------

現代的なLinuxディストリビューションの場合は以下のコマンドを入力するだけでインストールできます。

``` {.shell}
pip3 install labelImg
labelImg
labelImg [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Dockerの場合
------------

``` {.shell}
docker run -it \
--user $(id -u) \
-e DISPLAY=unix$DISPLAY \
--workdir=$(pwd) \
--volume="/home/$USER:/home/$USER" \
--volume="/etc/group:/etc/group:ro" \
--volume="/etc/passwd:/etc/passwd:ro" \
--volume="/etc/shadow:/etc/shadow:ro" \
--volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
-v /tmp/.X11-unix:/tmp/.X11-unix \
tzutalin/py2qt4

make qt4py2;./labelImg.py
```

あとは[サンプル動画](https://youtu.be/nw1GexJzbCI) を見るだけです。

定義済みクラスを作成するには？
------------------------------

[data/predefined\_classes.txt](https://github.com/tzutalin/labelImg/blob/master/data/predefined_classes.txt)
を編集してください。

ショートカット一覧
------------------

  -------------------- --------------------------------------------
  Ctrl + u             そのディレクトリの画像を読み込む

  Ctrl + r             アノテーションの生成ディレクトリを変更

  Ctrl + s             保存する

  Ctrl + d             現在選択している矩形トラベルをコピー

  Ctrl + Shift + d     現在表示している画像を削除

  Space                現在の画像に検証済みフラグを立てる

  w                    矩形を生成する

  d                    次の画像へ移動する

  a                    前の画像へ移動する

  del                  選択した矩形を削除

  Ctrl++               画像を拡大

  Ctrl\--              画像を縮小

  ↑→↓←                 十字キーで矩形を移動する
  -------------------- --------------------------------------------

開発に参加するには？
--------------------

このリポジトリにPull Request を送ってください。
