# mouseHover: Plugin API Docs

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Plugin](https://docs.coronalabs.com/plugin/)
| __Corona Store__     | [mouseHover](http://store.coronalabs.com/plugin/mouseHover)
| __Keywords__         | 
| __See also__         | 

## Overview

Hi there! Welcome to the documentation for [__Mouse Hover__](http://store.coronalabs.com/plugin/mouseHover). 

Mouse Hover is a plugin for [Corona](https://coronalabs.com/products/corona-sdk/) projects that are targeting __macOS__ and __Windows__. The plugin allows you to detect when the mouse cursor is hovering over display objects by adding a `mouseHover` event listener to them. 

Corona doesn't appear to support such hover detection out of the box and we kind of needed it. We put some code together and it seemed to work pretty ok, so we're sharing it as a plugin. Hope you like it. If you don't [let us know](https://github.com/BTNSG/plugin-mouseHover#support) what we can change.

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
			publisherId = "sg.btn",
		},
	},		
}
``````

## How it works

To use Mouse Hover in your project, 

1. `require` the plugin in your code.
2. Add a `"mouseHover"` event listener to the display object that needs to react to hovering.
3. Handle the hover events in your listener function. 

For an example of these steps, take a look at the [sample code](https://github.com/BTNSG/plugin-mouseHover#sample-code) below. 

The `mouseHover` event captures the state of hovering by reporting a `"began"`, `"moved"` or `"ended"` phase (`event.phase`). The event also provides a reference to the target object (`event.target`) and the cursor location (`event.x_` and `_event.y_`). 

The propogation of `mouseHover` events honors Corona's layered [drawing model](https://docs.coronalabs.com/guide/graphics/group.html#drawmodel). The event starts at the foremost display object and works its way back. Children of a display group receive the event before their parent. As the event propagates, if any of the objects along the way `return true` in their event listeners, the propagation is stopped.


Objects that are not visible (i.e. [object.isVisible](https://docs.coronalabs.com/api/type/DisplayObject/isVisible.html) set to false) and objects with an [alpha value](https://docs.coronalabs.com/api/type/DisplayObject/alpha.html) of 0 do not ordinarily receive `mouseHover` events. If you do want such objects to detect hovering, set their [isHoverTestable](isHoverTestable.markdown) property to `true`.



## Tips

* Consider using Spiral Code Studio's [Mouse Cursor](https://marketplace.coronalabs.com/plugin/mouse-cursor) plugin along with Mouse Hover to hint at what actions a user can perform. 



## Gotchas

* Just like display objects, display groups can also listen for `mouseHover` events. However, only those groups that [anchor their children](https://docs.coronalabs.com/api/type/GroupObject/anchorChildren.html) will receive them. This was done because groups that do not anchor children extend to infinity in all directions and would always test positive for a hover.

* Mouse Hover doesn't keep track of other events that may be occurring simultaneously (for e.g. [touch or tap](https://docs.coronalabs.com/guide/events/touchMultitouch/index.html) events that may occur along with the hover). The plugin also doesn't check for whether the mouse has been [clicked](https://docs.coronalabs.com/api/event/mouse/isPrimaryButtonDown.html) before dispatching `mouseHover` events. Keep this in mind if you are responding to such events in addition to `mouseHover`.

* We use Corona's [mouse events](https://docs.coronalabs.com/api/event/mouse/index.html) to test for hovering. So all the limitations of mouse events will apply.

* When Mouse Hover is `require`d it modifies Corona's `display.newPolygon` method such that every polygon object stores a reference to its array of of vertices under `object.vertices`. If you use any other code that also modifies `display.newPolygon` and assigns something other than the array of vertices to `object.vertices`, then Mouse Hover may not work properly.

* Mouse Hover may behave unpredictably in the case of [invalid polygon objects]](https://docs.coronalabs.com/api/library/display/newPolygon.html). These include self intersecting polygons or polygons with any duplicated vertex co-ordinates.

* In the case of images, _mouseHover_ events are dispatched if the cursor is anywhere within the image's rectangular frame. Mouse Hover cannot tell which part of the image is transparent and which has colored content.



### Note: Propagation protocol for overlapping objects

>Consider the case of two partially overlapping objects A and B with B being in front of A. Both the objects respond to _mouseHover_ events but only B returns `true` in its event listener. Say the mouse is hovering over A only, and is then moved onto the overlapping zone. As soon as this happens, B starts receiving the _mouseHover_ event with in the _"began"_ phase, while A receives one last _mouseHover_ event with the phase being _"ended"_. 




### Sample Code

``````lua
-- This code draws a funky star shaped thingy and has it light up when the mouse hovers over it

--* REQUIRE THE PLUGIN *--

local mouseHover = require 'plugin.mouseHover' -- the plugin is activated by default. 


--* DRAW A FUNKY STAR *--

local halfW = display.contentWidth * 0.5
local halfH = display.contentHeight * 0.5
local defaultAlpha = 0.4

local vertices = { 100,-110, 127,-35, 205,-35, 143,16, 165,90, 80,5, 100-65,90, 100-43,15, 100-105,-35, 100-27,-35}
 
local o = display.newPolygon( halfW, halfH, vertices )
o.fill = {0.2,0.2,0.7}
o.alpha = defaultAlpha
o.xScale = 6
o.yScale = 4

o.rotation = 20

--* DEFINE THE EVENT LISTENER FUNCTION *--

local onMouseHover = function(event)
	if event.phase == "began" then
		event.target.isVisible = true
		event.target.alpha = 1
		

	elseif event.phase == "ended" then

		event.target.alpha = defaultAlpha

	end

	-- not returning true

end

--* SIGN UP FOR mouseHover EVENTS *--

o:addEventListener( "mouseHover", onMouseHover )



-- that's it. 

``````

### Support

If you have any questions about Mouse Hover, please post them on the [plugin forum](http://btn.sg). If you want to reach out to us directly, feel free to [drop us an email](mailto://info@btn.sg) =)


## Compatibility

| Platform                     | Supported
| ---------------------------- | ---------------------------- 
| Mac App                      | YES
| Win32 App                    | YES
| Corona Simulator (Mac)       | YES
| Corona Simulator (Win)       | YES

