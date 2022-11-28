# LabelImg: Image annotation GUI built in PyQt

This is a fork of [Tzutalin's](https://github.com/tzutalin/) popular image annotation tool with slight modifications for improved efficiency and additional keyboard shortcuts. Tzutalin's LabelImg was recently taken over [heartexlabs](https://github.com/heartexlabs/). This fork will try to stay current with any significant heartexlabs improvements but will likely eventually diverge too much.

Recent changes:
- 27.11.2022
  + Add keypress for zoom to active annotation (`f`)
  + Add keypress for select next (`e`), previous (`w`), and iterate (`r`) annotation
  + Change `w` draw new box to `n`
  + Convert .rst to GH .md
- Previous changes by heartexlabs
  + Add Brighten, Darken, Optimal Brightness functions

Current known issues:
- [ ] `QAction::event: Ambiguous shortcut overload: Ctrl++` when using keyboard shortcut to zoom in

TODO:
- [ ] Update icons to FontAwesome
- [ ] Add GUI keyboard shortcut modal in GUI to avoid opening browser
- [ ] Rearrange all keyboard shortcuts
- [ ] Improve keyboard accessibility for label selection when using `CTL+E`
- [ ] Add numpad hotkeys for selecting < 11 annotations
- [ ] Add status widget with current anno, N annos in cur image, cur anno index
- [ ] Cleanup README: installation instructions, demo images, 


## About LabelImg

LabelImg is a graphical image annotation tool. It is written in Python and uses Qt for its graphical interface. Annotations are saved as XML files in PASCAL VOC format, the format used by [ImageNet](http://www.image-net.org/). Besides, it also supports YOLO and CreateML formats.

![Demo Image](demo/demo3.jpg)


### Installation Ubuntu Linux

Python 3 + Qt5

```shell
sudo apt-get install pyqt5-dev-tools
sudo pip3 install -r requirements/requirements-linux-python3.txt
make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

### Installation macOS

Python 3 + Qt5

```shell
brew install qt  # Install qt-5.x.x by Homebrew
brew install libxml2

# or using pip

pip3 install pyqt5 lxml # Install qt and lxml by pip

make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 Virtualenv (Recommended)

Virtualenv can avoid a lot of the QT / Python version issues

```shell
brew install python3
pip3 install pipenv
pipenv run pip install pyqt5==5.15.2 lxml
pipenv run make qt5py3
pipenv run python3 labelImg.py
# Optional]
rm -rf build dist; pipenv run python setup.py py2app -A; mv "dist/labelImg.app" /Applications
```

Note: The Last command gives you a nice .app file with a new SVG Icon in your /Applications folder. You can consider using the script: build-tools/build-for-macos.sh

### Installation Windows

Install [Python](https://www.python.org/downloads/windows/), [PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5) and [install lxml](http://lxml.de/installation.html). Open cmd and go to the [labelImg](#labelimg) directory

```shell
pyrcc4 -o libs/resources.py resources.qrc
For pyqt5, pyrcc5 -o libs/resources.py resources.qrc

python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

If you want to package it into a separate EXE file

```shell
# Install pyinstaller and execute:

pip install pyinstaller
pyinstaller --hidden-import=pyqt5 --hidden-import=lxml -F -n "labelImg" -c labelImg.py -p ./libs -p ./
```

### Windows + Anaconda

Download and install
[Anaconda](https://www.anaconda.com/download/#download) (Python 3+)

Open the Anaconda Prompt and go to the [labelImg](#labelimg) directory

```shell
conda install pyqt=5
conda install -c anaconda lxml
pyrcc5 -o libs/resources.py resources.qrc
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```


## Usage

Steps (PascalVOC)

1.  Build and launch using the instructions above.
2.  Click `Change default saved annotation folder` in Menu/File
3.  Click `Open Dir`
4.  Click `Create RectBox`
5.  Click and release left mouse to select a region to annotate the rect box
6.  You can use right mouse to drag the rect box to copy or move it

The annotation will be saved to the folder you specify.

You can refer to the below hotkeys to speed up your workflow.

## Steps (YOLO)

1.  In `data/predefined_classes.txt` define the list of classes that
    will be used for your training.
2.  Build and launch using the instructions above.
3.  Right below \"Save\" button in the toolbar, click \"PascalVOC\"
    button to switch to YOLO format.
4.  You may use Open/OpenDIR to process single or multiple images. When
    finished with a single image, click save.

A txt file of YOLO format will be saved in the same folder as your image with same name. A file named `classes.txt` is saved to that folder too. `classes.txt` defines the list of class names that your YOLO
label refers to.

Note:

- Your label list shall not change in the middle of processing a list of images. When you save an image, classes.txt will also get updated, while previous annotations will not be updated.
- You shouldn't use "default class" function when saving to YOLO format, it will not be referred.
- When saving as YOLO format, "difficult" flag is discarded.

## Create pre-defined classes

You can edit the [data/predefined\_classes.txt](data/predefined_classes.txt) to load pre-defined classes

Annotation visualization

1. Copy the existing lables file to same folder with the images. The labels file name must be same with image file name.
2. Click File and choose \'Open Dir\' then Open the image folder.
3. Select image in File List, it will appear the bounding box and label for all objects in that image.

(Choose Display Labels mode in View to show/hide labels)

## Hotkeys

| Key  | Action |
| --- | --- |
| Ctrl + u | Load all of the images from a directory |
| Ctrl + r | Change the default annotation target dir |
| Ctrl + s | Save |
| Ctrl + d | Copy the current label and rect box
| Ctrl + Shift + d | Delete the current image |
| Space | Flag the current image as verified |
| w | Create a rect box |
| d | Next image |
| a | Previous image |
| del | Delete the selected rect box |
| Ctrl++ | Zoom in |
| Ctrl\--  | Zoom out |
| ↑→↓← | Keyboard arrows to move selected rect box |


**Verify Image:**

When pressing space, the user can flag the image as verified, a green
background will appear. This is used when creating a dataset
automatically, the user can then through all the pictures and flag them
instead of annotate them.

**Difficult:**

The difficult field is set to 1 indicates that the object has been annotated as \"difficult\", for example, an object which is clearly visible but difficult to recognize without substantial use of context. According to your deep neural network implementation, you can include or exclude difficult objects during training.

## How to reset the settings

In case there are issues with loading the classes, you can either:

1.  From the top menu of the labelimg click on Menu/File/Reset All

2.  Remove the `labelImgSettings.pkl` from your home directory. In Linux and Mac you can do: `rm \~/.labelImgSettings.pkl`


## License

[Free software: MITlicense](https://github.com/tzutalin/labelImg/blob/master/LICENSE)

Citation: Tzutalin. LabelImg. Git code (2015). <https://github.com/tzutalin/labelImg>
