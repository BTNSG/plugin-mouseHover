__*[NOTE]:*__ See [Instructions](Instructions.markdown) for these stub documentation files. (Remove this before you deploy your docs)


# mouseHover: Plugin API Docs

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [TYPE](http://docs.coronalabs.com/api/type/Library.html)
| __Corona Store__     | [mouseHover](http://store.coronalabs.com/plugin/mouseHover)
| __Keywords__         | 
| __See also__         | 

## Overview

The mouseHover plugin can be used in your [Corona](https://coronalabs.com/products/corona-sdk/) project. It enables you to...


## Syntax

	local mouseHover = require "plugin.mouseHover"

### Functions

##### [mouseHover.loadTable()](loadTable.markdown)

##### [mouseHover.printTable()](printTable.markdown)

##### [mouseHover.saveTable()](saveTable.markdown)

##### [mouseHover.setScope()](setScope.markdown)

##### [mouseHover.FUNCTION()](FUNCTION.markdown)


### Properties

##### [mouseHover.PROPERTY](PROPERTY.markdown)

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

