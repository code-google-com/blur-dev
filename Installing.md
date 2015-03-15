# Installation Guide #

This page will walk you through how to install the BlurOffline system to your computer.




&lt;hr /&gt;



## Pre-Requisites ##

  * Windows

  * Python24  (for 32-bit components)
  * Python26  (for 64-bit components)

  * pywin32   (3rd party module)

  * Qt 4.6+   (32-bit/64-bit)
  * PyQt4     (32-bit/64-bit)

  * Visual Studio C++ Redistributable (For Max 2012)

There is no limitation on this if you wish to compile the code for yourself for different versions of Qt,PyQt, and/or Python.  We will only support the configurations that we require however.  To learn more about what to do, you need to read about the [Installed Source Code](InstalledSource.md)

Having trouble?  See the [FAQ](FAQ.md)

### Cross-platform Support ###

The frameworks that we work with (Python,Qt,PyQt) are all cross-platform, and all of the code that we have developed CAN be modified to support cross-platform (we have some working on Linux right now), however, we don't officially support it, as 3dsMax is our primary application, so we use Windows exclusively at Blur.

Perhaps in the future we'll support other platforms, right now however, we do not.

### How to get Python ###

For Python, its very easy - you simply have to go to http://www.python.org/ and find your binaries.  For your convenience, we've included links to the exact installers that we use:

  * [Python 2.4.4](http://www.python.org/ftp/python/2.4.4/python-2.4.4.msi)
  * [Python 2.6.6 (64-bit)](http://www.python.org/ftp/python/2.6.6/python-2.6.6.amd64.msi)

### How to get pywin32 ###

Some of our tools will use the pywin32 package for Python, which is a 3rd-party package that can be found here:

[pywin32](http://sourceforge.net/projects/pywin32/files/pywin32/)

Direct links to the latest Python24 x32 version are [here](http://sourceforge.net/projects/pywin32/files/pywin32/Build216/pywin32-216.win32-py2.4.exe/download).

Direct links to the latest Python26 x64 version are [here](http://sourceforge.net/projects/pywin32/files/pywin32/Build216/pywin32-216.win-amd64-py2.6.exe/download)

Here are some instructions to get Python up and running in Softimage if you have not already done so:

  * http://xsisupport.wordpress.com/2010/02/22/getting-python-to-show-up-in-softimage/

### How to get Qt ###

Qt is an open-source C++ framework originally developed by Trolltech, and now maintained by Nokia.

PyQt is a python wrapper on top of that framework.

If you do not have Qt/PyQt already installed, we actually provide the necessary Qt DLLs and PyQt packages for you in the BlurOffline install.

We ship:

  * Qt 4.6 DLLs for 32 & 64 bit
  * Qt Designer
  * Qt Assistant
  * PyQt for Python24 (32 bit)
  * PyQt for Python26 (64 bit)

If you want to get your own versions of Qt, you'll need:

  * [Qt](http://qt.nokia.com/products/)
  * [QScintilla](http://www.riverbankcomputing.co.uk/software/qscintilla/intro)
  * [PyQt4](http://www.riverbankcomputing.co.uk/software/pyqt/download)

## Installing BlurOffline ##

We have improved our installer system - so now it wraps all of the required modules into a single installer.  Well, 2 installers.  One installer for the 32-bit components, and one installer for the 64-bit components.

### Steps to Install ###

**Imporant Note: The paths for installs are hardcoded to our installation
paths at Blur, so you will need to navigate to the proper Python & 3dsMax paths for your computer.  Don't just assume that clicking "next" will install to the right location.**

  1. Download the version you want to install from [here](http://code.google.com/p/blur-dev/downloads/list)
  1. Save the file to your computer
  1. Run the installer
  1. Choose the components you wish to install
  1. Walk through the installers for other packages
  1. Thats it!

### Installed Components ###

This is just a quick overview of what each installed component includes, for more detailed information, look through the [component documentation](InstalledComponents.md).

#### Core Libraries ####

These are required libraries that are the base of our code

Installs the following packages

  * PYTHON\_PATH/lib/site-packages/blur
  * PYTHON\_PATH/lib/site-packages/blurdev

#### Qt Libraries ####

This will install the required Qt/PyQt components - if you already have these installed you can skip this section.  Note - for the 64-bit installation, you need to make sure to have write permissions for c:/Windows/system32

Installs Qt DLLs

For 32-bit, this will install:

  * c:/blur/common/
  * PYTHON24\_PATH/lib/site-packages/PyQt4

For 64-bit, this will install:

  * c:/Windows/system32/blur64/
  * PYTHON26\_PATH/lib/site-packages/PyQt4

#### Developer Tools ####

This will install the Qt Designer and Qt Assistant, as well as provide a link to the Blur IDE on the desktop.  The Blur IDE is the core development application defined in the blurdev/ide package and is used as the Python/PyQt editor for 3dsMax and Softimage.

For more information on the IDE editor, click [here](BlurIDE.md).

This will install:

  * c:/blur/common/designer.exe
  * c:/blur/common/assistant.exe
  * DESKTOP/Blur IDE

#### Tools and Source Code ####

This section will install all the Blur tools, as well as source code for all of the Blur DLLs that we have developed for 3dsMax and Softimage, including the source code for the blurPython DLL for 3dsMax.

**Note: This does not include the source code for Qt/PyQt as those can be found on the above links - we have not modified the code in anyway, simply compiled it for our needs.**

For more detailed information on this, see the [tools docs](Tools.md) and [source code docs](InstalledSource.md).

This will install:

  * c:/blur/dev/offline
  * DESKTOP/Treegrunt

#### 3dsMax Plugins ####

This will install all the required DLLs that we have made for 3dsMax.  This includes the blurPython DLL as well as additional DLLs that we have made over the years to extend Max.

Check off the ones you want to install, and it will install:

  * MAX\_PATH/plugins/blur
  * MAX\_PATH/stdplugs/stdscripts/baseLib/blurStartupMaxLib.ms
  * MAX\_PATH/scripts/python/
  * MAX\_PATH/scripts/startup/init\_python.ms

If everything works smoothly - you should see a Python menu in your 3dsMax right next to the Maxscript menu.

**Note: For later versions of 3dsMax (2010+), Autodesk started including Qt DLLs in their base installation, but were only including Qt 4.5.  To support our code, we're actually moving their DLLs out of the root folder to MAX\_PATH/bin/qt\_bak/  This will ensure that our DLLs are loaded, and they are backward compatible.  If, for any reason, something starts misbehaving, you can remove the above installed components, and copy the DLLs back out of that qt\_bak folder**

#### Microsoft Visual C++ 2010 Redistributable Package ####

For 3dsMax 2012 you will need to instal Microsoft's C++ redistributable dlls available here.

[64Bit](http://www.microsoft.com/download/en/details.aspx?id=14632)

[32Bit](http://www.microsoft.com/download/en/details.aspx?id=5555)


#### Softimage Plugins ####

You'll notice that there are no sections for installing Softimage plugins.  While 3dsMax requires localized DLL installs, we are using Softimage's Workgroups to control our plugin distribution.  So, to connect Softimage for Python & PyQt, you'll need to connect to:

  * c:/blur/dev/offline/workgroups/xsi\_blurdev

If you want to run the installed Blur Tools, you'll also need to connect to:

  * c:/blur/dev/offline/workgroups/xsi\_legacy

If that folder does not exist for some reason, its just short cut to:

  * c:/blur/dev/offline/maxscript/treegrunt/XSIWorkgroup

We're in the process of migrating and cleaning the code.

#### Offline Registration ####

This simply registers the proper offline configuration paths, it happens at the end to ensure that nothing overwrites the config settings.

Installs:

  * c:/blur/config.ini

## Supported Versions ##

  * Max2009 (32-bit/64-bit)
  * Max2010 (32-bit/64-bit)
  * Max2011 (32-bit/64-bit)

  * Softimage2010 (32-bit/64-bit)

  * **Coming Soon**
  * Softimage2012 (32-bit/64-bit)
  * Studiomax2012 (32-bit/64-bit)