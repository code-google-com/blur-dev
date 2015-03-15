# Frequently Asked Questions #

This is a list of all the most common questions about the Blur tools.




&lt;hr /&gt;



### Where are all the Treegrunt Tools? ###

The first time you run Treegrunt, you need to build the tools index that Treegrunt accesses.  There is a step by step process for it [here](Treegrunt.md).

### Nothing happens when I click an item in the 3dsMax Python menu? ###

If you do not do a standard install from the BlurOffline installer, then there are a couple of things that did not happen.

We have newer versions of the Qt DLLs that 3dsMax ships with (and are fully backward compatible), but the ones in the base Max folder clash with the ones that we use.  You have to move QtCore.dll, QtGui.dll and QtXml.dll from MAXPATH/**to MAXPATH/qt\_bak/**

That will force max to use the Qt DLLs that we have installed, and work with our code, instead of their own versions.  This should not affect anything in the program itself, if it does however, please report an issue, and you can always return the DLLs to the proper location to fix it (however breaking the Blur code).