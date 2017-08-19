# mouseHover.unRequire()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [mouseHover.*](Readme.markdown)
| __Return value__     | None



## Overview

When you no longer need to use the *mouseHover* plugin, you can _unrequire_ it by calling _mouseHover.unRequire()_. This function [deactivates](deactivate.markdown) the plugin and _nils_ out all the references to it in [package.loaded](https://docs.coronalabs.com/api/library/package/loaded.html).



## Syntax

	mouseHover.unRequire( )


## Note

In order for the _unrequiring_ to actually free up memory, you'll have to also _nil_ out any local references to the plugin that you may have created (see example below). Once you do this, the dangling tables that once pointed to the plugin should automatically get trashed by the [garbage collector](https://docs.coronalabs.com/api/library/global/collectgarbage.html). 

## Examples

``````lua
local myMouseHover = require 'plugin.mouseHover'

-- 11,532 lines of code later

myMouseHover.unRequire()
myMouseHover = nil

``````
