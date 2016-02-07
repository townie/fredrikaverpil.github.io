---
layout: post
title: Compiling PyQt5 for Python 2.7 on OS X
tags: [osx, python, pyqt]
---

I’m doing this on OS X 10.11 (El Capitan) using [Homebrew](http://brew.sh), so I'm really not compiling myself...

<!--more-->

In case you don’t have Homebrew installed:

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Let’s start with installing python, qt5, as well as wget using brew:

    brew install python qt5 wget

While that is “brewing”, make sure you have Xcode installed (can be installed via the [Mac App Store](https://itunes.apple.com/en/app/xcode/id497799835?mt=12)). When Xcode is installed, also make sure you have its command-line tools installed and that you have agreed to Apple’s license agreement:

xcode-select --install
sudo xcodebuild -license

Then let’s download the [PyQt5 source](https://riverbankcomputing.com/software/pyqt/download5) and the [SIP source](https://riverbankcomputing.com/software/sip/download).

    wget http://sourceforge.net/projects/pyqt/files/PyQt5/PyQt-5.5.1/PyQt-gpl-5.5.1.tar.gz
    wget http://sourceforge.net/projects/pyqt/files/sip/sip-4.17/sip-4.17.tar.gz

Double-check that the newly installed Python 2.7.x is being used when just executing python:

    python --version

Untar and compile (also double check the path to your qmake):

    tar -xvf sip-4.17.tar.gz
    cd sip-4.17
    python configure.py
    make
    make install

    cd..
    tar -xvf PyQt-gpl-5.5.1.tar.gz
    cd PyQt-gpl-5.5.1
    python configure.py --qmake=/usr/local/Cellar/qt5/5.5.1_2/bin/qmake
    make
    make install

Please note, you may want want to check out the options in the configure.py files prior to configuring/compiling.

You may now import PyQt5 as a module in Python 2.7!

    $ python

    Python 2.7.10 (default, Sep 23 2015, 04:34:21)
    [GCC 4.2.1 Compatible Apple LLVM 7.0.0 (clang-700.0.72)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import PyQt5
    >>>
