# Blur IDE Documentation #

Built using the QScintilla plugin for Qt for highlighting, the editor is a lightweight, yet powerful editing program that is cross-platform, as well as cross-application.

It runs as a standalone application, as well as a nested program within 3dsMax and Softimage for rapid development.




&lt;hr /&gt;



## Why another IDE? ##

The Blur IDE (Integrated Development Environment) is an open source code editing program with multi-language support.  The main ones that we use it for are Python, Maxscript, XML, HTML, Javascript, and CSS, but can support as many as QScintlla supports.

So, with many editors out there, why reinvent the wheel?

We had a couple of needs that we wanted to solve with the creation of our own editor.

  1. We needed an easy way to support non-standard languages (such as Maxscript) since we do development in a number of languages.
  1. We needed an editor that would work stand-alone...BUT ALSO inside of 3dsMax and Softimage to fully support our workflow
  1. We needed a test case for a complex application that CAN run inside of 3dsMax and Softimage with absolutely no code changes...
  1. We wanted a way to provide our TDs with a robust Wizard system to quickly create Tools and code without needing to remember all the ins and outs of the technical requirements.

## Where is it Installed? ##

The code for the IDE is actually installed as a sub-package within the blurdev python package.  This will be installed to:

```

PYTHON_PATH/lib/site-packages/blurdev/ide 

```

We are actively developing this editor, so we'll try to continue to roll out updates as we add useful features.  SO, if you choose to modify this code in anyway, I'd recommend doing it externally from this installed location so as to avoid any overwrites during a future upgrade.

One of the ideas we've had is adding a more robust plugin/addon system to the code so that external developers can add changes to it

## How do I use it? ##

### Pre-requisites ###

If you followed the [Installing](Installing.md) instructions, then you'll know that the pre-requisites for this are:

  1. Python
  1. Qt 4.6+
  1. QScintilla
  1. PyQt4

### Running Standalone ###

To run the IDE standalone, you should have installed the Development Tools section from the Installers, and now see a Blur IDE or Blur IDE\_64 link on your desktop.

If you don't, no worries - you can just create a link to the IDE directly:

```
PYTHON_PATH\pythonw.exe PYTHON_PATH\lib\site-packages\blurdev\runtimes\ide_editor.py
```

Where, ` PYTHON_PATH ` is the location that you installed the blurdev package to.

### Running from 3dsMax ###

To run the IDE from 3dsMax, make sure that you have setup your Py3dsMax system properly.  The instructions for that can be found [[here](Py3dsMax.md)].

All you have to do is choose ` Python >> Show IDE Editor `, and this will launch the editor as a child window of 3dsMax and you can start developing in [Python for Max](Py3dsMax.md)!

### Running from Softimage ###

To run the IDE from Softimage, make sure that you have setup your PySoftimage system properly.  The instructions for that can be found [[here](PySoftimage.md)].

All you have to do is choose ` Python >> Show IDE Editor `, and this will launch the editor as a child window of Softimage and you can start developing with [PyQt for Softimage](PySoftimage.md)!

## What comes in the Blur IDE? ##

### IDE Editor ###

The IDE Editor is the main window that you see.  This is the "base" application for the IDE system, however, it is all integrated.

All of the code runs through the base blurdev system, for instance, you can actually program the IDE Editor IN the editor itself...which, we do quite frequently.

Try this.

With the Editor open, hit F2, or go to {{{ Tools >> Show Logger }}.

### Logger Window ###

This will bring up the interactive Python console logger, which you can type Python commands on the fly - this is the same console that will run externally, as well as in Max and Softimage (which we'll see in the other tutorials).

Now, we can access the ide itelf:

```
>>> import blurdev
>>> ide = blurdev.core.ideeditor()
>>> ide.setWindowTitle( 'Testing' )
```

You should now see the editor's title has changed to ` 'Testing' `.

```
>>> ide.documentNew()
```

We just created a new document!  How fun...

All of the source code for the IDE is found in the blurdev/ide package, and takes advantage of other libraries developed within the blurdev package.

Feel free to check out the SDK for hit by hitting F1 or choosing ` Help >> SDK Help `.

### SDK Window ###

This will bring up the SDK Window.  What the SDK Window is, is a Python based help document generator.

The first time you run it, you'll have to specify the SDK file to load, so choose this one:

```
PYTHON_PATH/lib/site-packages/blurdev/resource/sdk/blurdev.sdk
```

It doesn't really "generate" the documentation (like Doxygen does) as much as dynamically generate the HTML for the content on the fly.

It only works for Python (at the moment), but works by importing python modules and using the built-in python documentation inspection methods to generate code documentation on the fly.

What that means is, the moment your code changes - your documentation is up to date.

The only caveat of this, is that if a module cannot be imported, it cannot be documented...which, may or may not be a good thing.

## Creating a Project ##

### Create a project for BlurOffline ###

So, lets create a simple project in the IDE now, and so everyone has the same code to start with - lets make a project for the BlurOffline code.

In the IDE Editor, go to ` Project >> New Project `

The first field will contain the path to your project file's location - this is where the ` *.blurproj ` file will be saved.  This will default to the standard blur location: ` c:/blur/dev ` for Windows, but you can save your project file wherever you want.

In the ` project name ` field, type ` BlurOffline `.

This will update the first tree item to the match the title - as this will be the root item for your project.

From here, you have a few options - you can point the head item to an actual path, and it will just recursively add all the files/folders within that path, or you can create custom groups.

For now, we'll keep it simple.  Right-click on the ` BlurOffline ` tree item and choose ` Edit Item `.

Uncheck the ` custom group ` option, and for the ` path ` field, navigate to ` c:/blur/dev/offline/code `.

You can leave the rest of the settings the way they are and click **Ok**.

**Save** your project, and it will then switch your IDE to the BlurOffline project.

If you want to edit the settings for this at any time, you can always right-click on an item in the navigator tree, and choose ` Edit Project... `.

### Managing Multiple Projects ###

If you want to create other projects, the process is the same.

As your projects grow, you'll want to quickly be able to toggle between them - you can go setup your favorites by going to

```
Project >> Open Favorites...
```

From here, you can right-click and add any project you want as a favorite, then double-clicking on that will load it up.

This is a good, fast way to toggle between projects.

## Managing Preferences ##

You'll notice as you start doing more development, that even though the IDE is the same _code_, the _settings_ will change if you're in 3dsMax or Softimage.

This is because of the internal preference management system of the blurdev packages.

All user prefs for tools developed for the blurdev environment/treegrunt system, will save to:

```
c:/blur/userprefs/[application]/[pref]
```

The core system will know what application is being run, so tools, such as the IDE editor, will only know about their own preferences.  This way, you can setup different project favorites for 3dsMax from Softimage, from Standalone.

We'll delve into this more when we talk about [developing Tools](PyQt.md).