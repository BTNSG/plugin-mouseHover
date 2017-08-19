# mouseHover.setScope()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [mouseHover.*](Readme.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | None



## Overview

mouseHover checks for hover events on a particular group (the scope) and all its children. By default, the scope of the plugin is the entire Stage object. This works fine for most cases. However, if you only want to scan a specific display group for hover events, then you can change the scope by calling mouseHover.setScope() and passing that display group.

## Syntax

	mouseHover.setScope( displayGroup )

##### displayGroup <small>(required)</small>
_[GroupObject](https://docs.coronalabs.com/api/library/display/newGroup.html)._ The display group that you want to set as the scope for checking hover events.

## Note

	Display groups receive "mouseHover" events only when they anchor their children. This is because a group that does not anchor its children extends to infinity along both dimensions and would always test positive for a "mouseHover" event. 

	Independent of whether a group anchors its children or not, all the group's children are tested for "mouseHover" events

## Examples

``````lua
local mouseHover = require 'plugin.mouseHover'

local colors = mouseHover.setScope( "colors.json" )
``````
