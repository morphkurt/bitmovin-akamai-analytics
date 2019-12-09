# Connect the Bitmovin Adaptive Streaming Player with Akamai Analytics

This is a guide how to integrate Akamai analytics with Bitmovin player

### Include the standard Akamai Analytics Plugin

More information is covered in the Akamai Control center

JavaScript Plug-in Integration Guide>Integration Procedure>Data Management

```html
<script type="text/javascript" src="javascript_malibrary.js"></script>
```

### Initiate the AkamaiAnalytics object 

```html
// Note: Get Config Url from https://control.akamai.com/homeng/view/main (Configure > Media Analytics > Data Source > Configuration Steps:	View Steps)
// Should look something like http://ma1192-r.analytics.edgesuite.net/config/beacon-XXXXX.xml
var akamaiAnalyticsConfigUrl  = 'INSERT-CONFIG-PATH-HERE';
var akamaiAnalytics = new JS_AkamaiMediaAnalytics("http://media-analytics.akamaized.net/analyticsplugin/configuration/SampleBeacon.xml");
```

### Setup Custom Data

```html
var akamaiAnalytics = new JS_AkamaiMediaAnalytics("http://media-analytics.akamaized.net/analyticsplugin/configuration/SampleBeacon.xml");
// Setting Custom Data
akamaiAnalytics.setData("title", "Game Of Thrones - Season 1 Winter Is Coming");
akamaiAnalytics.setData("eventName", "Game Of Thrones - Season 1 Winter Is Coming");
akamaiAnalytics.setData("device", "iPhone 7");
akamaiAnalytics.setData("deliveryType", "L");
akamaiAnalytics.setData("cdn", "Akamai");
akamaiAnalytics.setData("category", "TV Shows");
akamaiAnalytics.setData("subCategory", "Fantasy Drama");
akamaiAnalytics.setData("show", "Game Of Thrones");
akamaiAnalytics.setData("contentLength", "3697"); // Value in seconds
akamaiAnalytics.setData("playerId", "SamplePlayer01");
akamaiAnalytics.setViewerId("uniqueIdentifier");
akamaiAnalytics.setViewerDiagnosticsId("diagnosticIdentifier");
akamaiAnalytics.disableServerIPLookUp();
akamaiAnalytics.disableLocation()

```

### Handling Player Events

Bitmovin player provides event handles where Akamai Analytics beacon can be fired off. Sample events to capture play / pause / seek / adstart / adskip / adfinish has been shown below

```javascript
   player.on('play', function (o) {
      log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handlePlaying()"  +++');
      if (akamaiAnalytics) {
        akamaiAnalytics.handlePlaying();
      }
    });
    player.on('paused', function () {
      log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handlePause()" +++');
      if (akamaiAnalytics) {
        akamaiAnalytics.handlePause();
      }
    });
    player.on("seeked", function () {
      if (akamaiAnalytics) {
        log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handleSeekStart()" +++');
        akamaiAnalytics.handleSeekStart();
      }
    });
    player.on("adstarted", function () {
      if (akamaiAnalytics) {
      var adInfoObject = {};
      adInfoObject["adDuration"] = adDuration; // duration is in milliseconds
      akamaiAnalytics.handleAdStarted(adObject);
      log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handleAdStarted" +++');  
      }
    });
    player.on("adskipped", function () {
      if (akamaiAnalytics) {
        akamaiAnalytics.handleAdSkipped()
      log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handleAdSkipped()" +++');  
      }
    });
     player.on("adfinished", function () {
      if (akamaiAnalytics) {
        akamaiAnalytics.handleAdComplete();
      log('+++ akamaiAnalytics beacon fired "akamaiAnalytics.handleAdComplete()" +++');  
      }
    });
    
    
    

```
