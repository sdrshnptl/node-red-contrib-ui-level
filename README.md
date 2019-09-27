# node-red-contrib-ui-level

[![NodeRed](https://img.shields.io/badge/Node--Red-0.19.4+-red.svg)](http://nodered.org)
[![NPM version][npm-image]][npm-url]
[![CodeFactor](https://www.codefactor.io/repository/github/hotnipi/node-red-contrib-ui-level/badge)](https://www.codefactor.io/repository/github/hotnipi/node-red-contrib-ui-level)

[npm-image]: http://img.shields.io/npm/v/node-red-contrib-ui-level.svg
[npm-url]: https://npmjs.org/package/node-red-contrib-ui-level

Adds a linear Level type widget to the user interface

![node-red-dashboard-ui-level.JPG](img/node-red-dashboard-ui-level.JPG)


# Requirements
Node-Red v19.4 or greater. 
Node-Red-dashboard v2.13.0 or greater. 
For best user experiences it is reccomended to use Node-Red-dashboard v2.15.0 or creater.
# Configuration and behavior
Widget has 3 different layouts: Single Horizontal, Pair Horizontal and Single Vertical.

Takes the `msg.payload` and displays the value at the top of the level graphics.
For Pair Horizontal layout the `msg.payload` is expected to be an `array`
`msg.payload` is validated to find a nummeric value. So you can send number `msg.payload = 15` or string `msg.payload = "15"` 

The node's `Label` is displayed near the value. Leave the label field empty to show value only.
For Pair Horizontal layout the `Label` is not displayed but both `Channels` can be labelled independently.

All four colors for stripes can be customized. In adition there is three options to show the colors. `Multiple segments` - Colors tied to stripes according to sector values. `Single color bar` - Single value based color for all active stripes. `Interpolated colors` - Colors interpolated from normal to high color.
If you choose `Multiple segments` for your stripe colors, you can optionally use the `Peak mode`. By selecting the `Peak mode`, you can adjust `peak hold` time (in milliseconds, validated to be in between 800 ... 10000)

The node's `Unit` will be displayed near the current value. Exact position of the unit depends on choosed layout. The unit can be any `string`, for example: `lbs psi F°` Set the unit to empty string if you don't need to display it.

The min and max values are customizable within the configuration or you can change them on fly by sending new values with `msg.control` property.

The segments's values are also customizable within the configuration and with `msg.control`

You can choose anmations to be `Soft`, `Reactive` or `Rocket` represending speed of animations (800ms, 300ms and 100ms). Animations can be turned `off` completely.
Animation of value text is turned off by default. You can turn it on but be aware, text animation affects
performance significantly!



You can choose between 3 different stripe resolutions. `Superfine`, `Fine` and `Normal`

Texts sizes and color in widget can be customized within the configuration only. Color applies for all texts in widget. There is 3 different sizes for text elements in use. Values represent font relative size with unit `"em"`

## Examples of `msg.control` usage

`msg.control = {min:10, max:80}` _to change min and max values._

`msg.control = {min:10, max:80, seg1:30, seg2:60}` _to change min, max and segments all together._

`msg.control = {seg2:60}` _to change high segement value only._

If peak mode used, it can be turned to hold peak permanently and then reset peak manually. 
`msg.control = {peakreset:"reset"}` _to turn on permanent hold or if already in this mode, just reset peak._

`msg.control = {peakreset:"auto"}` _to change peak mode delay based._

## Performance alert
This widget is not perfect choice to display high-frequent data changes like audio or similar.  
If you are using a lot of Level widgets on your dashboard and you are feeling performance loss, considere  turning off animations of value text (if used) or turn off all animations. 
