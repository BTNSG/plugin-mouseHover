#object.isHoverTestable

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Boolean]
| __Library__          | [mouseHover.*](Readme.markdown)
| __Keywords__         | PROPERTY
| __See also__         | 


## Overview

Objects that are not visible (i.e. [object.isVisible](https://docs.coronalabs.com/api/type/DisplayObject/isVisible.html) set to false) and objects with an [alpha value](https://docs.coronalabs.com/api/type/DisplayObject/alpha.html) of 0 do not ordinarily receive *mouseHover* events. If you do want such an object to be able to detect a hover, set *object.isHoverTestable* to `true`.


## Example
 
``````lua
local mouseHover = require 'plugin.mouseHover'

local rect = display.newRect(0,0,100,200)
rect.alpha = 0
rect.isHoverTestable = true

local hoverListener = function(event)

	print(event.phase, event.x, event.y)
end

rect:addEventListener("mouseHover", hoverListener)
``````
