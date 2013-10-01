wemonode
========

A Node.js framework for managing Belkin Wemo socket and sensor

IMPORTANT:
Remember to change "upnpBindAddress" in wemonode_config.json file


Usage example:
```javascript


/* Requiring WemoNode module */
var WemoNode = require('wemonode');

/* Getting an instance */
var wemoNode = WemoNode.WemoNode();



/* Listening to "device_found" event.
    WemoNode will fire this event every time a new device is detected.
    If the detected device is a socket, then set the binary state to 1 (turn on)
*/
wemoNode.on("device_found", function (object) {

    if (object.deviceType == 'socket')
        wemoNode.sendCommand("socket_setbinarystate", object, {"binarystate": 1});


}.bind(this));



/* Listening to "device_lost" event.
    WemoNode will fire this event every time a device stops responding for 30 seconds.
 */
wemoNode.on("device_lost", function (object) {
}.bind(this));



/* Listening to "state_changed" event.
    WemoNode will fire this event every time a device changes its internal status.
 */
wemoNode.on("state_changed", function (object) {
    console.log("State changed emitted from " + object.id + " binaryState:" + object.binarystate);
}.bind(this));


var turnOffWemoSwitch = function(object){
    wemoNode.sendCommand("socket_setbinarystate", object, {"binarystate": 0});
}


wemoNode.startDiscovery();

setTimeout(wemoNode.stopDiscovery,10000);
```
