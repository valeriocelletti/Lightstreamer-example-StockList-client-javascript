
Lightstreamer StockList Demo Client for JavaScript
==================================================

This project includes different demos based on Lightstreamer StockList Adapter:

* Basic Stock-List Demo
* Stock-List Demo
* Framed Stock-List Demo
* Bandwidth and Frequency Demo
* Simple Grid Demo
* Chart Demo

Basic StockList Demo
---------------------

This demo displays real-time market data for ten stocks, generated by a feed simulator.<br>
This page uses the JavaScript Client API for Lightstreamer to handle the communications with Lightstreamer Server. A simple user interface is implemented to display the real-time data received from Lightstreamer Server. The front-end code is kept extremely simple and represents a good introduction to Lightstreamer subscription management. In particular, the client code can be considered as a reference example of item subscriptions in MERGE mode.

The demo includes the following client-side technologies:
* A [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 10 items, subscribed to in MERGE mode feeding a [StaticGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/StaticGrid.html).

StockList Demo
---------------

This demo shows some further features with respect to the Basic Stock-List Demo.<br>
Click on the stock names to open pop-up windows that display real-time streaming charts. Notice that the maximum update frequency set for the pop-up windows is greater than the frequency set for the main window. The data is resampled by Lightstreamer Server according to the maximum frequency requested by each table (you can easily notice that if you open "Ations Europe").<br>
Click on the link under the table (Next/Previous 15) to dynamically switch between two lists of fifteen items, without losing previously opened pop-ups. If you open the same demo in different browser windows, you will see slightly different values for the most updated stocks. Again, this behavior shows how the data resampling is done in real-time on a per-window basis.
Notice that a large portion of the JavaScript front-end code is devoted to client-side formatting operations.

The demo includes the following client-side technologies:
* A [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 15 items, subscribed to in MERGE mode feeding a [DynaGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/DynaGrid.html).
* For each pop-up window opened, a [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 1 item, subscribed to in MERGE mode feeding both a [StaticGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/StaticGrid.html) and a [Chart](http://www.lightstreamer.com/docs/client_javascript_uni_api/Chart.html).

Framed StockList Demo
---------------------

The same as the Stock-List Demo, but with a different architecture for the LightstreamerClient integration.<br>
A LightstreamerClient object is always kept alive in a hidden page. For an explanation of the different deployment strategies please refer to the "JavaScript Client Guide.pdf" document.

The demo includes the following client-side technologies:
* A [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 15 items, subscribed to in MERGE mode feeding a [DynaGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/DynaGrid.html).
* For each pop-up window opened, a [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 1 item, subscribed to in MERGE mode feeding both a [StaticGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/StaticGrid.html) and a [Chart](http://www.lightstreamer.com/docs/client_javascript_uni_api/Chart.html).

Bandwidth and Frequency Demo
----------------------------

The Bandwidth and Frequency Demo demonstrates two important features of Lightstreamer: bandwidth management and frequency management.<br>
Use the Max Bandwidth slider to dynamically change the maximum bandwidth granted to for the current session. The client will notify the server of the new bandwidth and the server will change the update frequency on the fly, in order to respect the bandwidth limit.
You can see that with a bandwidth as ridiculous as 0.5 kilobits per seconds, Lightstreamer is still able to deliver updates to the page, thanks to the very optimized network protocol used.<br>

Use the Max Frequency slider to dynamically change the maximum update rate of each item in the Subscription. The client will notify the server of the new frequency limit and the server will change the update frequency on the fly, in order to respect the frequency limit.<br>

You can see how the bandwidth and frequency constraints act on different levels. The bandwidth constraint is applied to the whole session, that is, to the global update flow for this page. On the other hand, the frequency constraint is applied to each row (Item) individually. Both the constraints set an upper bound, which is dynamically managed by Lightstreamer Server.
Note that thanks to MERGE mode, the updates are not queued and delayed, but resampled and conflated. In other words, when an item has a chance to be updated (based on a round-robin algorithm), it will receive the very latest state available, not an old one.<br>

Click on the link under the table (Next/Previous 15) to dynamically switch between two lists of fifteen items and see how the initial snapshot is loaded still respecting the bandwidth limit.

The demo includes the following client-side technologies:
* Two [Subscriptions](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 15 items each, subscribed to in MERGE mode feeding a [DynaGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/DynaGrid.html) alternately according to the selected list.

Simple Grid Demo
----------------

This demo shows how it is possible to build a "dynamic-subscription grid" by leveraging a Lightstreamer DynaGrid.<br>
The 30 items of the Stock-List Demo are virtually contained in the grid, but only 5 at a time are displayed. The slider to the right implements a virtual scroll bar. When the table is scrolled, the invisible items are unsubscribed from and the new visible items are subscribed to. To accomplish this, each Lightstreamer Subscription contains one item only and each row on the DynaGrid is fed by a different Lightstreamer Subscription: the granularity of subscriptions and unsubscriptions is at the row level.<br>
This technique enables to handle visual grids containing thousands of items with a very low impact on both the client side and the server side.

The demo includes the following client-side technologies:
* A [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) for each visible row, containing 1 item, subscribed to in MERGE mode. All of the Subscriptions feed the same [DynaGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/DynaGrid.html).

Chart Demo
----------

This demo shows the capability of Lightstreamer to plot some simple real-time streaming charts in pure HTML and JavaScript. This feature is also demonstrated in the pop-up windows of the Stock-List Demo. For more sophisticated charts, it is possible to use third-party charting libraries.<br>
In this chart, the prices for two stocks are normalized to 100 and plotted.

The demo includes the following client-side technologies:
* A [Subscription](http://www.lightstreamer.com/docs/client_javascript_uni_api/Subscription.html) containing 2 items, subscribed to in MERGE mode feeding a [StaticGrid](http://www.lightstreamer.com/docs/client_javascript_uni_api/StaticGrid.html) and a [Chart](http://www.lightstreamer.com/docs/client_javascript_uni_api/Chart.html).

Run The Demos
-------------

Before you can run the demos of this project some dependencies need to be solved:

-  Get the lightstreamer.js file from the [Lightstreamer 5 Colosseo distribution](http://www.lightstreamer.com/download) 
   and put it in the src/[demo_name]/js folder of the demo (if that is the case, please create it). Alternatively you can build a lightstreamer.js file from the 
   [online generator](http://www.lightstreamer.com/distros/Lightstreamer_Allegro-Presto-Vivace_5_0_Colosseo_20120803/Lightstreamer/DOCS-SDKs/sdk_client_javascript/tools/generator.html).
   In that case be sure to include the LightstreamerClient, Subscription, DynaGrid, StaticGrid, Chart, SimpleChartListener, and StatusWidget modules and to use the "Use AMD" version.
-  Get the require.js file form [requirejs.org](http://requirejs.org/docs/download.html) and put it in the src/[demo_name]/js folder of the demo.
-  This apply only for Bandwidth and Frequency Demo and Simple Grid Demo. Get the zip file from [script.aculo.us](http://script.aculo.us/downloads) and put the prototype.js, scriptaculous.js, and slider.js files in the src/[demo_name]/js/scriptaculous folder of the demo.

You can deploy these demos in order to use the Lightstreamer server as Web server or in any external Web Server you are running. 
If you choose the former case please note that in the <LS_HOME>/pages/demos/ folder there is a copy of some of the src/[demo_name] directories of this project, in other cases please create the folders <LS_HOME>/pages/demos/[demo_name] then copy here the contents of the src/[demo_name] folder of this project.<br>
The client demos configuration assumes that Lightstreamer Server, Lightstreamer Adapters and this client are launched on the same machine. If you need to targeting a different Lightstreamer server please search this line:
```js
var lsClient = new LightstreamerClient(protocolToUse+"//localhost:8080","DEMO");
```
in lsClient.js or index.html, depending on the demo, and change it accordingly.<br>
Anyway the [QUOTE_ADAPTER](https://github.com/Weswit/Lightstreamer-example-Stocklist-adapter-java) and [LiteralBasedProvider](https://github.com/Weswit/Lightstreamer-example-ReusableMetadata-adapter-java) have to be deployed in your local Lightstreamer server instance. The factory configuration of Lightstreamer server already provides this adapter deployed.<br>
The demos are now ready to be launched. You can find demostrations hosted in our servers [here](http://www.lightstreamer.com/demos).

See Also
--------

* [Lightstreamer StockList Demo Adapter](https://github.com/Weswit/Lightstreamer-example-Stocklist-adapter-java)
* [Lightstreamer Reusable Metadata Adapter in Java](https://github.com/Weswit/Lightstreamer-example-ReusableMetadata-adapter-java)

Lightstreamer Compatibility Notes
---------------------------------

- Compatible with Lightstreamer JavaScript Client library version 6.0 or newer.