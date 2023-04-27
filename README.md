DX is an open IOT specification that is simple and lightweight for easy implementation. It's designed based on the MQTT protocol for real-time data exchange. The payload format is concise for high performance consideration.


### Path

The basic path to publish or subscribe should be based on the following structure:


```
<VER>/<RSV>/<SRC>/<DST>/<EVT>
```


&lt;VER> The current version of prefix of the path is always started by `xda.json:` 

&lt;RSV> The currently empty `//` and is reserved for customization use, hence the topic subscription should be started by `xda.json:/+/`.

&lt;SRC> is the self defined name of the data source, which can be a name of a driver, device, etc.

&lt;DST> is the self defined name of the data destination, it could be a targeted device, group name, security role, etc.

&lt;EVT> is the event or category name whereby the real-time data will be using `onchange`, and historical data will be using `onlog`.

A typical DX path may be published to:


```
xda.json://DEMO.abc/grp/onchange
```


And to receive the real time data from any parties, the subscription path should be:


```
xda.json:/+/+/+/onchange
```



### Payload

The DX payload is designed in JSON format for browser's direct use and the data types are simplified to numbers, string and Boolean, which is native in JavaScript. Below is one typical example:


```
{"tag1":[[t1,v1],[t2,v2],,,[tn,vn]],"tag2":[[t1,v1],[t2,v2],,,[tn,vn]],,,}
```


The t & v in the sample are representing time and values. There's no additional status indication but using native `null` to indicate bad data/status. 

NOTE: 

The key-value pairs payload format can be readily processed using JavaScript [object.entries()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) and [object.fromEntries()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries).
