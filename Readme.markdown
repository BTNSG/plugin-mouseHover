# mouseHover: Plugin API Docs

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Plugin](https://docs.coronalabs.com/plugin/)
| __Corona Store__     | [mouseHover](http://store.coronalabs.com/plugin/mouseHover)
| __Keywords__         | 
| __See also__         | 

## Overview

__mouseHover__ is a plugin for [Corona](https://coronalabs.com/products/corona-sdk/) projects that are targeting Windows and macOS. The plugin allows you to detect when the mouse cursor is hovering over display objects simply by adding a "mouseHover" event listener to them. 

The *mouseHover* event has a *"began"*, *"moved"* and an *"ended"* phase. The event also passes on the cursor location as _event.x_ and _event.y_.

The propogation of the _mouseHover_ event honors Corona's layered [drawing model](https://docs.coronalabs.com/guide/graphics/group.html#drawmodel). The event starts at the foremost display object and works its way back. If any of the objects along the way `return true` in their event listeners, the propogation is stopped.

Display groups can also listen for *mouseHover* events, but only groups that [anchor their children](https://docs.coronalabs.com/api/type/GroupObject/anchorChildren.html) will receive them. This is because groups that do not anchor children extend to infinity in all direction and would thus always test positive for a hover.

Objects that are not visible (i.e. [object.isVisible](https://docs.coronalabs.com/api/type/DisplayObject/isVisible.html) set to false) and objects with an [alpha value](https://docs.coronalabs.com/api/type/DisplayObject/alpha.html) of 0 do not ordinarily receive *mouseHover* events. If you do want such an object to be able to detect a hover, set its [isHoverTestable](isHoverTestable.markdown) property to `true`.

## Syntax

	local mouseHover = require "plugin.mouseHover"

### Functions

##### [mouseHover.setScope()](setScope.markdown)


### Properties

##### [object.isHoverTestable](isHoverTestable.markdown)

## Project Configuration

### Corona Store Activation

In order to use this plugin, you must activate the plugin at the [Corona Store](http://store.coronalabs.com/plugin/mouseHover).


### SDK

When you build using the Corona Simulator, the server automatically takes care of integrating the plugin into your project. 

All you need to do is add an entry into a `plugins` table of your `build.settings`. The following is an example of a minimal `build.settings` file:

``````
settings =
{
	plugins =
	{
		-- key is the name passed to Lua's 'require()'
		["plugin.mouseHover"] =
		{
			-- required
			publisherId = "REVERSE_btn.sg",
		},
	},		
}
``````

### Enterprise

If you have activated this plugin, you can download this plugin from the corresponding plugin page in the [Corona Store](http://store.coronalabs.com/plugin/mouseHover).


## Platform-specific Notes

[Insert discussion on issues specific to iOS/Android/etc, or to specific devices]


## Resources

### Sample Code

You can access sample code [here](SAMPLE_CODE_URL).

### Support

More support is available from the BTN Pte Ltd team:

* [E-mail](mailto://info@btn.sg)
* [Forum](http://btn.sg)
* [Plugin Publisher](http://btn.sg)


## Compatibility

| Platform                     | Supported
| ---------------------------- | ---------------------------- 
| iOS                          | No
| Android                      | No
| Android (GameStick)          | No
| Android (Kindle)             | No
| Android (NOOK)               | No
| Android (Ouya)               | No
| Mac App                      | YES
| Win32 App                    | YES
| Windows Phone 8              | No
| Corona Simulator (Mac)       | YES
| Corona Simulator (Win)       | YES

