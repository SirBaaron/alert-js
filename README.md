# alert-js
A small js library for alerts

<br><br>

####View a demo [here](http://sirbaaron.github.io/alert-js/demo/)

<br>

Alert-js is an easy way to integrate userfriendly, smoothly animated, in material design held alerts. Use them to display important information that needs to be seen NOW and let the user take actions. The action buttons have ripple effects, which are also styleable. You can show alerts with one function call and detect the clicked action just as easily. Users can also dismiss an alert by pressing `esc` and click the right-most action with `enter`. If you try to show an alert while one is already open, it gets stored in a queue and shown after the current one gets closed.

<br><br><br>

### Setup
**With npm:**<p>1. At the root of your index, type `npm install alert-js` into the command line.<br>2. Add the tag `<script src="node_modules/alert-js/alert.min.js"></script>` to your index file. If you want to show alerts on finished load, also add the script tag `<script src="node_modules/ripple-js/ripple.min.js"></script>` BEFORE!

<br><br><br>
### Properties

* **accentColor** `string`<br>Sets the color of the action buttons and also the ripple effect for all future alerts<p>°Corresponds to the css `color` and `ripple-color` property. Click [here](https://github.com/SirBaaron/ripple-js#properties) for more information<br>°_Example:_ `alert.accentColor = "green";`<br>°_Default value:_ `"orange"`
* **rippleOpacity** `Float`<br>Change the opacity of the ripple for all future alerts<p>°Corresponds to the `ripple-opacity` property. Click [here](https://github.com/SirBaaron/ripple-js#properties) for more information<br>°_Example:_ `alert.rippleOpacity = 0.3;`<br>°_Default value:_ `0.6`
* **ripplePressExpandTime** `Float`<br>Change how long the ripple takes to fully expand while it is being pressed for all future alerts<p>°Corresponds to the `ripple-press-expand-time` property. Click [here](https://github.com/SirBaaron/ripple-js#properties) for more information<br>°_Example:_ `alert.ripplePressExpandTime = 3.3;`<br>°_Default value:_ `1.5`
* **rippleReleaseExpandTime** `Float`<br>Set in which time the ripple completes the ripple when the user lets go of it for all future alerts<p>°Corresponds to the `ripple-release-expand-time` property. Click [here](https://github.com/SirBaaron/ripple-js#properties) for more information<br>°_Example:_ `alert.rippleReleaseExpandTime = 0.5;`<br>°_Default value:_ `0.3`
* **rippleLeaveCollapseTime** `Float`<br>Change how long the ripple takes to cancel<p>°Corresponds to the `ripple-leave-collapse-time` property. Click [here](https://github.com/SirBaaron/ripple-js#properties) for more information<br>°_Example:_ `alert.rippleLeaveCollapseTime = 0.1;`<br>°_Default value:_ `0.4`
* **open** `Boolean` `read-only`<br>True, when an alert is open and false otherwise<p>°_Example:_ `var isAlertOpen = alert.open;`

<br><br><br>
###Methods

* **show()**<br>Call this function to display an alert. If an alert is already open, it gets stored in the queue<p>°**Parameters:**<br>&nbsp;&nbsp;<b>text:</b>  `String`<br>&nbsp;&nbsp;&nbsp;&nbsp;The text the alert should display. You can use html elements and style attributes just like in the document.<br>&nbsp;&nbsp;<b>actions:</b>  `Array of Strings` `optional`<br>&nbsp;&nbsp;&nbsp;&nbsp;For every entry a corresponding button will be displayed in the alert. If ommited or empty, only an "OK" button will be displayed<br>&nbsp;&nbsp;<b>options:</b> `Object` `optional`<br>&nbsp;&nbsp;&nbsp;&nbsp;If you don't want to apply the global options to this alert, you can change the settings for only this alert with all properties (except open) described [here](https://github.com/SirBaaron/alert-js#properties). Possible example: `{accentColor: "blue", rippleOpacity: 0.7}`<br>&nbsp;&nbsp;<b>mode</b> `String` `optional`<br>&nbsp;&nbsp;&nbsp;&nbsp;Change how the queue should behave with one of the three following options:<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_"replace"_ This clears the queue, closes the old alert and instantly shows the new one<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_"next-in-queue"_ Instead of putting the alert at the end of the queue, this places the alert as the next one in the waiting queue<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"_next_" Use this to show the new alert instantly instead of the current one, but preserve the queue<br>°**Return value:**<br>&nbsp;&nbsp;The function returns a Promise, which resolves to the action the user clicked. See the examples for working code<br>°**Examples:**<br>&nbsp;&nbsp; -`alert.show("Hello world");` The most simple form of an alert.<br>&nbsp;&nbsp;-`alert.show("We couldn't find your position for one of the following reasons:<ul><li>Your device doesn't support gps</li><li>You didn't grant us access to your position</li><li>The device can't find it's position</li></ul>");` You can use html tags just as you would expect.<br>&nbsp;&nbsp;-`alert.show("Do you want to switch to our mobile website?", ["No", "Yes"]);` While you should build responsive websites, this approach is also possible.<br>&nbsp;&nbsp;-`alert.show("If you prefer green more...", [], {accentColor: "green"});` How to change the settings for only this alert. Note how `actions` is empty, so only "OK" will be displayed.<br>&nbsp;&nbsp;-`alert.show("This information is so important that it needs to be displayed instantly, instead of all other alerts!", [], {}, "replace");` This will clear the queue and display the alert instantly.<br>&nbsp;&nbsp;-`alert.show("Dou you want to delete this photo? There is no going back!", ["Cancel", "OK"]).then(function(action) { if(action == "OK") { //delete the photo }});` Detect what action the user clicks with this pattern.
* **hide()**<br>Use this to hide the alert without that the user needs to take an action.<p>°_Example:_ `alert.hide();`
* **clearQueue()**<br>This does what it sound like, it clears the queue of waiting alerts.<p>°_Example:_ `alert.clearQueue();`

<br><br><br>
### Tips & Notes

* If you wan to hide the current alert and also the one in the queue, call `alert.clearQueue();` before calling `alert.hide();`.
* This library uses my other library, ripple-js, which you can find [here](https://github.com/SirBaaron/ripple-js).
* If you use ripple-js otherwhere in your project or want to show alerts on page load, import `ripple-js` before importing `alert-js`. If those uses don't fit your use case, you don't need to import `ripple-js`, as it will be imported automatically.
* If you don't want to have a ripple effect, set `rippleOpacity` to `0`.
