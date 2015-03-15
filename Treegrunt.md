# Treegrunt #

The Treegrunt is the main entry point to all of the Blur tools.  It is an environment and tool management system that allows a TD to quickly develop and deploy tools to artists.




&lt;hr /&gt;



## Where are all the Tools? ##

So if this is the Tool launching system...where are all the tools?  For offline installations, the first time you run the Treegrunt you'll have to update its index.

### Updating the Tools Index ###

If you don't see any tools, or if you are a Developer who created a new tool, in your Treegrunt:

  1. Right-click in Treegrunt
  1. Choose ` Environments >> Rebuild Index `
  1. Hit OK on the popup dialog

This will rebuild the XML index of tools that Treegrunt uses to launch tools from.

### Why do I need to do this? ###

Originally, the Treegrunt system simply looked through the folder system for tools.

As our tools and necessities became more complex, we needed a faster and more flexible system, so we went with an XML based "database" of tools.  This is a much faster system as it doesn't have to troll the filesystem every time it needs to look for tools.

The XML file provided a single place to lookup all tools, and allowed us to build a generic way to define Tools to register to the system.

To learn more about adding tools to the treegrunt, look through the [tools tutorial](PyQt.md).

## How do I run Treegrunt? ##

### External Treegrunt ###

Just double-click the Treegrunt link on your DESKTOP.  This will run Treegrunt with any tools registered as External.

### 3dsMax Treegrunt ###

Choose `Python >> Treegrunt`.  This will run Treegrunt with any tools registered as Studiomax and Legacy Studiomax.

### Softimage Treegrunt ###

Choose `Python >> Treegrunt`.  This will run Treegrunt with any tools registered as Softimage and Legacy Softimage.