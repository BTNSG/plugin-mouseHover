# mouseHover.setScope()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [mouseHover.*](Readme.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | None



## Overview

_mouseHover_ works by cycling through a group and all the group's children to see if the cursor is hovering over any of them. We call this group the _scope_ of the _mouseHover_ plugin.

By default the scope is set to Corona's display [stage](https://docs.coronalabs.com/api/type/StageObject/index.html). However, if you only want to scan a specific display group and its children for hover events and not the entire stage, you can change the _scope_ by calling mouseHover.setScope() and passing that specific display group.

## Syntax

	mouseHover.setScope( displayGroup )

##### displayGroup <small>(required)</small>
_[GroupObject](https://docs.coronalabs.com/api/library/display/newGroup.html)._ The display group that you want to set as the _scope_ for checking hover events.

## Note

Display groups can listen for *mouseHover* events, but only those groups that [anchor their children](https://docs.coronalabs.com/api/type/GroupObject/anchorChildren.html) will receive them. This was done because groups that do not anchor children extend to infinity in all directions and would always test positive for a hover. This applies for the _scope_ display group as well.

Of course, all of the _scope_'s children are tested for _mouseHover_ events independent of whether the _scope_ anchors its children or not,.

## Examples

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
