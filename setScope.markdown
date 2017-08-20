# mouseHover.setScope()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [mouseHover.*](Readme.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | None



## Overview

_mouseHover_ works by cycling through all the child display objects of a particular group, checking to see if the cursor is hovering over any of them. We call this group the _scope_ of the _mouseHover_ plugin.

By default the scope is set to Corona's display [stage](https://docs.coronalabs.com/api/type/StageObject/index.html). However, if you only want to scan a specific display group's children for hover events and not the entire stage, you can change the scope by calling mouseHover.setScope() and passing it the specific display group.

## Syntax

	mouseHover.setScope( displayGroup )

##### displayGroup <small>(required)</small>
_[GroupObject](https://docs.coronalabs.com/api/library/display/newGroup.html)._ The display group that you want to set as the _scope_ for checking hover events.

## Example

``````lua
local mouseHover = require 'plugin.mouseHover'

local halfW = display.contentWidth * 0.5
local halfH = display.contentHeight * 0.5


local testGroup = display.newGroup()
testGroup.anchorChildren = true
testGroup.x = halfW
testGroup.y = halfH

testGroup:addEventListener( "mouseHover", groupHoverListener )

local circle = display.newCircle(halfW*0.5, halfH*0.5, halfW*0.1)
circle.rotation = -50
circle.fill = {0,0.3,0.4}
circle.alpha = defaultAlpha
circle.xScale = 5
circle.yScale = 1.5

testGroup:insert(circle)

local onCircHover = function(event)
	print("circleHover", event.phase)
end

circle:addEventListener( "mouseHover", onCircHover )
``````
