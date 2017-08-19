# mouseHover.activate()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [mouseHover.*](Readme.markdown)
| __Return value__     | None
| __See also__         | [mouseHover.deactivate()](deactivate.markdown)


## Overview

This activates the Runtime event listener used by the plugin to check for hover events. Note that the plugin is activated by default when you `require` it. You'd only ever have to call this function if you had previously deactivated the listener by using [mouseHover.deactivate()](deactivate.markdown)



## Syntax

	mouseHover.activate( )


## Examples

``````lua
local myMouseHover = require 'plugin.mouseHover' -- the plugin is activated by default. 

-- 2,032 lines of code later

myMouseHover.deactivate() -- this removes the plugin's Runtime listener

-- 5,421 lines later

myMouseHover.activate() -- this adds the plugin's Runtime listener back again


``````
