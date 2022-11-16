PySide 6.4.0.1 + PyInstaller bug demo
===

# tldr:

When you run `script.py` directly it works as expected.
When you build a pyinstaller dist, it fails on startup with the following exception:
```
$ dist/script/script
Traceback (most recent call last):
  File "script.py", line 31, in <module>
    window = MainWindow()
  File "script.py", line 21, in __init__
    button_action.setShortcut(QKeySequence(Qt.AltModifier | Qt.Key_D))
TypeError: unsupported operand type(s) for |: 'KeyboardModifier' and 'Key'
```

# To reproduce

I'm using Python 3.10.8 that I built from source:
```
./configure --enable-optimizations --prefix=/opt/python3.10.8 --enable-shared
make -j16
sudo make install
```

I make a venv:
```
/opt/python3.10.8/bin/python3 -m venv 310
source 310/bin/activate
pip install -r requirements.txt
```

Then I can run `python script.py` and it works as expected.
However, if I build a pyinstaller distribution with `pyinstaller script.py`, the resulting executable (`dist/script/script`) raises the above exception and exits without displaying anything.

