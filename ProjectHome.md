# 2.7.2014 - Project moved to sourceforge #

Because google groups has disabled adding new downloads, we are moving to Source Forge.

# [Click here to go to PROJECT on SourceForge](http://sourceforge.net/projects/blur-dev) #

# 12.5.2013 - Max 2014 support added #

Adds the long awaited Max 2014 support.

It has Qt fully integrated and is compatible with the current caddies.gup. To do this we had to modify caddies.gup and MaxQtBridge.dll to point to the standard Qt dll names, and not the custom _AD_ dlls. Qt had to be compiled with msvc2010(previous versions of max required msvc2008). If you have max 2014 installed along side older versions of max it will install the msvc2008 versions of Qt/PyQt/Blur\_Python into the standard locations(Ours are, c:\windows\system32\blur64, and c:\python27\lib\site-packages), and the msvc2010 Qt/PyQt/Blur\_Python into the max folder(C:\Program Files\Autodesk\3ds Max 2014, C:\Program Files\Autodesk\3ds Max 2014\scripts\python\site-packages). If you are re-distributing the installers yourself, make sure to pass the Qt installer the /noRegisterPath argument to prevent adding the max path to the system path environment variable.

Note: Blur has skipped Max 2013 so it has been dropped from the installer. I have added a download for the current build of Py3dsMax for python 2.7. We have also moved entirely to Python 2.7.

# 1.28.2013 - Fix for two Py3dsMax plugins being installed #

There was a bug in the last installer. It would install two versions of the Py3dsMax plugin and the plugin for python 2.7 would take precedence. This version will fix that problem. Make sure you uninstall the old version before installing.

# 1.16.2013 - Tool restructure #

Re-structured the tools folder structure. You may need to rebuild the treegrunt index.
All non-legacy tools are now located in c:\blur\dev\offline\code\python\tools instead of various sub folders of that location. The installer will **remove the existing offline folder**, so if you have added any new tools you will need to back them up before hand.

Added support for environment variables for tool user guides and studio name. This controls the prefix for macros in StudioMax and Softimage, an the url used to show tool documentation. for These can be edited by setting environment variables, or updating [PythonFolder](PythonFolder.md)\Lib\site-packages\blurdev\resource\settings.ini

```
bdev_studio_name = Blur
bdev_user_guide_url = http://redmine.blur.com/projects/pipeline/wiki/%s
bdev_default_author_email = beta@blur.com
```

Added lib folders for specific versions and of python. You can add any .pyd's or other files that are python version specific.
\code\python\lib\_python26, \code\python\lib\_python26\_64, \code\python\lib\_python27\_64

# 4.25.2012 - Installer Overhaul #

Overhaul of the installer to simplify the install experience. It now checks for the proper installs of python and pywin32 and if not found it will install them. It will select the installed versions of 3dsMax**by default, and default to the correct install location. It now patches pywin32 to work with xsi.**

Removed the installers for Qt-Dev and Classmaker, this drops about 88 megs from the installer size. These installers will be provided separately.

Unified the various uninstallers into a single uninstaller.

NSIS shared library is now included with in the tools install so rebuilding installers is possible again.

Py3dsMax.AtTime bug fixes.

**Currently automatic selection and path finding only works with the English version of max.**

# 2.14.2012 - New Release #

Thanks to Matt N. for making updates to the Py3dsMax plugin. There have been several changes to memory management that should make it much more stable.
He also made it possible to use "at time" from python by calling Py3dsMax.AtTime

```
from Py3dsMax import AtTime
at = AtTime()
at(10)
at(20)
del(at) # remove the at time functionality. As long as the at object exists it will be applied.
```

### blur3d ###

  * Depreciated blur3d.api.SceneWrapper.setName. Use blur3d.api.SceneWrapper.setDisplayName instead.
  * Depreciated models, cameras, _nativeModels,_nativeCameras from blur3d.api.Scene. Use blur3d.api.Scene.object specifying type instead.
  * Moved all commands from blur3d.api.enum into blur3d.constants

### BlurIDE ###

  * File monitoring for open files.
  * Fixed explorer context menu for edit with BlurIDE
  * The IDE will now open files with a UNC file path. (\\server\share\file.py)

### blurdev ###

  * importing blurdev will add c:\windows\system32\blur64 or c:\blur\common to the qt library paths.

Rember to check your paths when installing. They are currently hard coded to Blur's file system. Hopefully I can get this working off the registry for the next release.

# 10.17.2011 - blurdev updated #

Updated the installers with the latest version of blurdev. This includes many upgrades to the IDE.

We also moved a few commands from blur3d.api.Scene into blur3d.api.Application.

  * Moved Scene.softwareName() to Application.name()
  * Moved Scene.softwareID() to Application.id()
  * Moved Scene.softwareVersion() to Application.version()
  * Moved Scene.softwareNameAndVersion() to Application.nameAndVersion()


# 07.22.2011 - Max 2012 Supported #

Thanks to Mike H. for getting the blurPython DLL compiled for Max 2012!  This is still in BETA phase, but is publically available for download.

So, give it a go when you get a minute!

# 05.04.2011 - Back up! #

Well - that took considerably longer than anticipated...I apologize for that.

We are back though!  We now have a much more sophisticated and tested system as we have been using it production for over a year now.  Right now we support Max 2008-2011 and are actively working on supporting 2012, and while we have the Python support working, we have to recompile the rest of our DLLs for all the Blur Tools to work.

Check out the [Installation Guide](Installing.md) for info on how to get the code up and running, along with more tutorials on how to use the system.

Blur Dev Team

**Note: We do not support the old BlurBeta plugins, they are supported by a different team who are not directly related to Blur Studio anymore**

# Blur Studio - Development #

[Blur Studio](http://www.blur.com) has long been a proponent of sharing its programming resources, and in keeping with that tradition, we have opened up this project to share our innovations with the public.

### Disclaimer ###

This is our production code, we're releasing it out publicly, but as read-only for the time being as we are not equipped to handle multiple trunks and code changes coming from outside of the studio.  All the code is being released "as-is", if it doesn't work, feel free to make an issue, and we will try to address it as we can, but we have limited resources, and as we are not a software house, this is not the primary goal of the studio - unsupported versions and operating systems will be considered very low priority for us as our number 1 priority is making sure our code works here at the studio.

### Who is this site for? ###

  * Artists - _We have a wealth of tools and utilities designed to help the artist work_
  * TDs - _Our libraries can help bridge the gap between art and code_
  * Developers - _The frameworks presented can open a whole new world of possibility_