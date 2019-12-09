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

```
addEventHandler('play', function(data) { 
  if (akamaiAnalytics){
    akamaiAnalytics.handlePlaying();
  }
});
addEventHandler('pause', function(data) { 
  if (akamaiAnalytics){
    akamaiAnalytics.handlePause();
  }
});
```
