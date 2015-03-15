# Introduction to PyQt #

If you are completely new to Python and/or PyQt, then I would recommend working through some online tutorials - there are a TON of them out there.

This tutorial is about working with PyQt as it relates to the Blur systems, not a basic introduction to PyQt in general.

The tutorials on this page are for generic development - everything in these docs can and does apply to code for 3dsMax and Softimage - as the system we developed is application agnostic.




&lt;hr /&gt;



## Pre-requistes ##

I'm assuming that you've read through the [BlurIDE](BlurIDE.md) documentation and are setup with the BlurOffline code project.

## Hello, World ##

Everyone's favorite - Hello World.

For this example, we'll go into a couple of differences between the basics of PyQt and the system that we have in place.

First up, fire open your IDE Editor (can be standalone, or in an application of choice) and make sure we are in the BlurOffline project.

Click ` Ctrl+N ` or ` File >> New ` and type:

```
from blurdev.gui import Dialog

class HelloWorldDialog(Dialog):
    def __init__( self, parent = None ):
        Dialog.__init__( self, parent )
        
        self.setWindowTitle('Hello, World')

import blurdev
blurdev.launch(HelloWorldDialog)
```

Save this file to ` c:/blur/dev/offline/code/python/scripts/test.py `

### Dialog vs. QDialog ###

The first thing to note, is our first line.
```
from blurdev.gui import Dialog
```

We're importing our own ` Dialog ` class, not a standard ` PyQt4.QtGui.QDialog ` class.

In fact, the ` Dialog ` class inherits from the standard ` QDialog ` class, but it also provides some important wrapper code around it.  The wrapper code works with the blurdev/core logic to determine the proper parenting based on the application it's running in.

When standalone, no parent is needed, but if running within 3dsMax for instance, a Dialog MUST be a child of a ` QWinWidget ` class.  Rather than making the developer check for the proper parenting, we just wrote our own base class to support it.

We did this for the 3 base classes that we'll use when developing tools:

  * `blurdev.gui.Dialog` vs. `PyQt4.QtGui.QDialog`
  * `blurdev.gui.Window` vs. `PyQt4.QtGui.QWindow`
  * `blurdev.gui.Wizard` vs. `PyQt4.QtGui.QWizard`

A couple of notes about the differences between the 3:

  1. A Dialog can be run modally
  1. A Window contains a menu bar by default, but cannot be run modally
  1. A Wizard will drive a multi-step process.

This is obviously a dumbed down version of the differences between the 3, but is most often what drives our decision when to use each.

### blurdev.launch ###

The next thing to note from this example is the way that we run the tool.

The last line of code for this example calls
```
blurdev.launch(HelloWorldDialog)
```

What the `blurdev.launch` code is doing for us is managing the QApplication system.

In a standard PyQt application, a developer would have to maintain their application instance, however, there can only ever be 1 instance of a QApplication running per thread.

In the case of 3dsMax and Softimage, we'll have 1 QApplication instance running for ALL tools that are created.  When we're running standalone though, we're going to have 1 QApplication PER tool.

Again, to abstract our code to be able to work in multiple applications, it was easiest to build the system into the core to maintain the application instancing.

By calling `blurdev.launch` on your dialog, this will allow you to develop a tool that can run both IN and OUT of another application.

**Note: You only need to do this for your root dialogs.  If you have say, an About dialog that is a sub-dialog of your main Tool, you can just show it in a standard Qt way**.

### Running the Example ###

So, what does this all mean?  Lets give it a test.

  1. Navigate to `python/scripts` in your IDE
  1. Right-click on `test.py` and choose `Run`

This will launch your dialog, and you'll notice that it is parented to the IDE Editor (if running standalone) or your application window (if running in 3dsMax or Softimage).

This is because its running within the current thread, which already has a QApplication instance running, and so parents to the root window.

Now try:

  1. Right-click on `test.py` and choose `Run (Standalone)`

This will run your script as its own application - so it actually creates a full standalone application, creating its own QApplication and runs within its own thread.

This now runs outside of the IDE editor and/or application.

**Note: if you are building tools that need to access information inside of an application like 3dsMax or Softimage, they CANNOT access the Py3dsMax or PySoftimage libraries, so you have to program accordingly.**

**Note 2: if you choose `Run (Debug)` it is the same as running standalone, except that you'll get the command prompt window as well.**

## Building Tools ##

Before we get into developing tools, you should read up on how the [a tool is structured](ToolsEnvironments.md).

Once you have a grasp of what a Tool _is_, lets create a more advanced script than our Hello, World example from above - this time, lets create a new tool.

### Creating Categories ###

  1. Navigate to `BlurOffline/code/python/tools/General_Use_Tools`
  1. Right-click on `General_Use_Tools` and choose `New Folder`
  1. Type in `_Examples`

This will create a new folder at:
```
c:/blur/dev/offline/code/python/tools/General_Use_Tools/_Examples
```

Thats all you have to do to create a new category - create a new folder within the `tools` folder.

**Note: For readability, its recommended to start categories with an underscore.**

### Creating Tools ###

You could create a folder the way you just did, and then create a `__meta__.xml` file within it with the proper settings...but thats just not fun...

### IDE Tool Wizard ###

Instead of forcing a developer to remember everything that goes into a Tool, it was much easier to build a Wizard that we could reuse.

With that in mind, we built a robust and extensible wizard system into the IDE Editor.

We have wizards for creating more Wizards, creating tools Environments, gui components, and for Tools.

This time, right click on your `_Examples` folder and choose `New From Wizard`

This will bring up the Wizard chooser dialog.  Since right now we're creating a new tool, lets choose:

`User Interface` and then `Tool`

The Wizard you'll see will give you a couple of options.

  * The button on the left will let you choose the icon for your tool
  * Name field will be the name of your tool
  * Choosing simple script will build the tool with no GUI, and just register code to run within your `main.pyw`
  * Base Class field lets you choose from the 3 basic Tools UI options (Dialog,Window,Wizard)
  * Create Ui File will alter whether or not to create a Qt Designer file for you GUI, or if you want to define it programmatically
  * Description is just the tooltip for your new tool
  * ToolTypes registers where this tool can be run from.  As we'll show, you can actually develop a single tool that can run in 3dsMax, Softimage and External applications.  Extensions for Maya and Houdini are easily created, we just don't support them at Blur.

For now, lets set:

  * **name** SampleTool
  * **toolTypes** External, Studiomax, Softimage
  * **description** Sample tool for learning the IDE

We'll leave the other settings as they are by default (if you want to choose an icon, go ahead and do so).

  * Click `Continue`

The next page you'll see will outline the files and folders that will be created for your wizard.  You'll see this as the last page for all IDE Wizards, so you can always preview your files before you create them.

Only checked files will be created, so if for whatever reason you don't need or want certain files or folders, you can disable them through this view.

If you want to see the difference between what gets created, you can click back and toggle the **simple script** and/or **create ui file** fields, and this will alter the template for the tool that gets created.

For now, we'll just create with the standard settings, so click `Done`

You'll then be prompted if you want to change projects - when a tool gets created, it actually makes a new IDE Project specifically for that tool.

For now, click no - we'll just stay in the current project.

### Running the Tool ###

If you expand the `_Examples` folder, you'll now see your `SampleTool` tool folder, and all the files from the Wizard are setup for you.

If you right click on the `main.pyw` file and choose any of the three:

  1. Run
  1. Run (Standalone)
  1. Run (Debug)

You can see your tool running as a child of the IDE Editor, and/or as a standalone application.

All you'll see right now is a blank Dialog with the title `SampleTool`

### Modifying the Interface ###

Pretty simple to get started, but also boring.

Lets add a few GUI components.

  1. Navigate to `BlurOffline/python/tools/General_Use_Tools/_Examples/SampleTool/ui`
  1. Double-click on `sampletooldialog.ui'

This should open the Qt Designer with your UI file.

**Note: If you're not using the standard blur installed version of designer, you can register your version to the IDE by setting the `BDEV_QT_DESIGNER' value in `PYTHON\_PATH/lib/site-packages/blurdev/resource/settings.ini' to the path of your Designer.**

Otherwise, you can drag & drop the file from the IDE Editor into an open instance of the Designer.

We aren't going to go into Qt Designer tutorials - there are plenty of those online.

Instead, I'll just say add 3 components: add a tree named "uiBrowserTREE", a button called "uiLoadBTN", and a button called "uiSaveBTN".

It doesn't matter how its layed out for the sake of this tutorial, as long as the components are created and named properly.

Save the UI, and rerun the code.  You'll now see your tool with your components - without having to change any code!

### Running through Treegrunt ###

So now that you have your tool - you'll want to be able to register it to treegrunt.

If you run Treegrunt, you'll notice that your Tool doesn't popup.  Whenever you modify the tools structure (add a tool, move a tool, rename a tool) you'll actually have to rebuild your XML index file.

Right-click on the Window and choose `Environments >> Rebuild Index`

Now you'll find `General_Use_Tools >> Examples >> SampleTool` and you can double-click on it to run it.

Thats all you have to do to register the tool to the system, the wizard took care of the rest.