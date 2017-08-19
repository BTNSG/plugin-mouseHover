# mouseHover: Plugin API Docs

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Plugin](https://docs.coronalabs.com/plugin/)
| __Corona Store__     | [mouseHover](http://store.coronalabs.com/plugin/mouseHover)
| __Keywords__         | 
| __See also__         | 

## Overview

Hi there! Welcome to the documentation of [__Mouse Hover__](http://store.coronalabs.com/plugin/mouseHover). 

Mouse Hover is a plugin for [Corona](https://coronalabs.com/products/corona-sdk/) projects that are targeting __Windows__ and __macOS__. The plugin allows you to detect when the mouse cursor is hovering over display objects simply by adding a _mouseHover_ event listener to them. For some reason, Corona doesn't appear to support such hover detection out of the box. We kind of needed the ability to check for mouse hovers. We put some code together and it seemed to work pretty ok, so we're sharing it as a plugin. Hope you like it. If you don't [let us know](https://github.com/BTNSG/plugin-mouseHover#support) what we can change.

## Syntax

	local mouseHover = require "plugin.mouseHover"

### Functions

##### [mouseHover.setScope()](setScope.markdown)

##### [mouseHover.activate()](activate.markdown)

##### [mouseHover.deactivate()](deactivate.markdown)

##### [mouseHover.unRequire()](unRequire.markdown)


### Properties

##### [object.isHoverTestable](isHoverTestable.markdown)

## Setting up

In order to use this plugin, you need to activate the plugin at the [Corona Store](http://store.coronalabs.com/plugin/mouseHover). When you build using the Corona Simulator, the server automatically takes care of integrating the plugin into your project. 

All you need to do is add an entry into a `plugins` table of your `build.settings` like so:

``````
settings =
{
	plugins =
	{
		["plugin.mouseHover"] =
		{
			-- required
			publisherId = "btn.sg",
		},
	},		
}
``````

## How it works

The *mouseHover* event has a *"began"*, *"moved"* and an *"ended"* phase. The event also passes on the target object (_event.target_) and the cursor location (_event.x_ and _event.y_). Simply add a `"mouseHover"` event listener to a display object and handle the hover event however you like in your listener function. Take a look at the [example] below. 

The propogation of the _mouseHover_ event honors Corona's layered [drawing model](https://docs.coronalabs.com/guide/graphics/group.html#drawmodel). The event starts at the foremost display object and works its way back. Children of a display group receive the _mouseHover_ event before their parent. As the event propagates, if any of the objects along the way `return true` in their event listeners, the propagation is stopped.



## Tips

* Consider using Spiral Code Studio's [Mouse Cursor](https://marketplace.coronalabs.com/plugin/mouse-cursor) plugin along with __Mouse Hover__ to hint at what actions a user can perform. 



## Gotchas

* Display groups can listen for *mouseHover* events, but only those groups that [anchor their children](https://docs.coronalabs.com/api/type/GroupObject/anchorChildren.html) will receive them. This was done because groups that do not anchor children extend to infinity in all directions and would always test positive for a hover.

* _mouseHover_ events don't have any knowledge of [touch and tap](https://docs.coronalabs.com/guide/events/touchMultitouch/index.html) events that may be occurring simultaneously. Keep this in mind in case you're responding to those events in addition to _mouseHover_.

* The plugin also doesn't check for whether the mouse has been [clicked](https://docs.coronalabs.com/api/event/mouse/isPrimaryButtonDown.html) before dispatching _mouseHover_ events. Again, keep this in mind if you are responding to such [mouse events](https://docs.coronalabs.com/api/event/mouse/index.html) in addition to _mouseHover_.

* We use Corona's [mouse events](https://docs.coronalabs.com/api/event/mouse/index.html) to test for hovering. So all the limitations of mouse events will apply.

* In the case of images, _mouseHover_ events are dispatched if the cursor is anywhere within the image's rectangular frame. This is 'cause we didn't find a way to test for which parts of the image are transparent and which have content (if you know how to do that, we'll be happy to add this in).



#### Propagation protocol for overlapping objects

>Consider the case of two partially overlapping objects A and B with B being in front of A. Both the objects respond to _mouseHover_ events but only B returns `true` in its event listener. Say the mouse is hovering over A only, and is then moved onto the overlapping zone. As soon as this happens, B starts receiving the _mouseHover_ event with in the _"began"_ phase, while A receives one last _mouseHover_ event with the phase being _"ended"_. 

Objects that are not visible (i.e. [object.isVisible](https://docs.coronalabs.com/api/type/DisplayObject/isVisible.html) set to false) and objects with an [alpha value](https://docs.coronalabs.com/api/type/DisplayObject/alpha.html) of 0 do not ordinarily receive *mouseHover* events. If you do want such objects to detect hovering, set their [isHoverTestable](isHoverTestable.markdown) property to `true`.



### Sample Code

``````lua
-- main.lua

local mouseHover = require 'plugin.mouseHover' -- the plugin is activated by default. 

local halfW = display.contentWidth * 0.5
local halfH = display.contentHeight * 0.5

local defaultAlpha = 0.4

local onMouseHover = function(event)
	if event.phase == "began" then
		event.target.isVisible = true
		event.target.alpha = 1
		

	elseif event.phase == "ended" then

		event.target.alpha = defaultAlpha

	end

	-- not returning true

end


local vertices = { 100,-110, 127,-35, 205,-35, 143,16, 165,90, 80,5, 100-65,90, 100-43,15, 100-105,-35, 100-27,-35}
 
local o = display.newPolygon( halfW, halfH, vertices )
o.fill = {0.2,0.2,0.7}
o.strokeWidth = 5
o:setStrokeColor( 0, 0, 0 )
o.alpha = defaultAlpha
o.xScale = 3
o.yScale = 2

o.rotation = 20
o:addEventListener( "mouseHover", onMouseHover )

``````

### Support

If you have any questions about __Mouse Hover__, please post them on the [plugin forum](http://btn.sg). If you want to yell at us directly, feel free to [drop us an email](mailto://info@btn.sg) =) Also, here's [our website](http://btn.sg)). (__Spoiler alert!__ Building Corona plugins isn't our raison d'etre) 


## Compatibility

| Platform                     | Supported
| ---------------------------- | ---------------------------- 
| Mac App                      | YES
| Win32 App                    | YES
| Corona Simulator (Mac)       | YES
| Corona Simulator (Win)       | YES

