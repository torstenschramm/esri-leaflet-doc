---
title: L.esri.Cluster.FeatureLayer
layout: documentation.hbs
---

# {{page.data.title}}

Extends [`L.esri.Layers.FeatureLayer`]({{assets}}api-reference/layers-feature-layer.html)

`L.esri.Cluster.FeatureLayer` provides integration for Feature Layers with the [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) plugin. Because of the extra dependency on Leaflet.markercluster we do not include `L.esri.Cluster.FeatureLayer` in the default build of Esri Leaflet.  You will also need to include your own copy of the [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) plugin.

More information about Feature Layers can be found in the [`L.esri.FeatureLayer`]({{assets}}api-reference/layers/feature-layer.html) documentation.

### Constructor

<table>
    <thead>
        <tr>
            <th>Constructor</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code class="nobr">L.esri.Cluster.featureLayer({{{param 'Object' 'options'}}})</code></td>
            <td>You must pass a <code>url</code> to a [Feature Layer](https://developers.arcgis.com/rest/services-reference/layer-feature-service-.htm) in your <code>options</code></td>
        </tr>
    </tbody>
</table>

### Options

<table>
    <thead>
        <tr>
            <th>Option</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
          <td><code>url</code></td>
          <td><code>String</code></td>
          <td><strong>Required</strong> The URL to the [Feature Layer](https://developers.arcgis.com/rest/services-reference/layer-feature-service-.htm).</td>
        </tr>
        <tr>
            <td><code>pointToLayer({{{param 'GeoJSON Feature' 'feature' 'https://tools.ietf.org/html/rfc7946#section-3.2'}}}, {{{param 'LatLng' 'latlng' 'https://leafletjs.com/reference.html#latlng'}}})</code></td>
            <td><code>Function</code></td>
            <td>Function that will be used for creating layers for GeoJSON points (if not specified, simple markers will be created).</td>
        </tr>
        <tr>
            <td><code>style({{{param 'GeoJSON Feature' 'feature' 'https://tools.ietf.org/html/rfc7946#section-3.2'}}}, {{{param 'ILayer' 'layer' 'https://leafletjs.com/reference.html#ilayer'}}})</code></td>
            <td><code>Function</code></td>
            <td>Function that will be used to get style options for vector layers created for GeoJSON features.</td>
        </tr>
        <tr>
            <td><code>onEachFeature({{{param 'GeoJSON Feature' 'feature' 'https://tools.ietf.org/html/rfc7946#section-3.2'}}}, {{{param 'ILayer' 'layer' 'https://leafletjs.com/reference.html#ilayer'}}})</code></td>
            <td><code>Function</code></td>
            <td> </td>
        </tr>
        <tr>
            <td><code>where</code></td>
            <td><code>String</code></td>
            <td>A server side expression that will be evaluated to filter features. By default this will include all features in a service.</td>
        </tr>
        <tr>
            <td><code>fields</code></td>
            <td><code>Array</code></td>
            <td>An array of fieldnames to pull from the service. Includes all fields by default. You should always specify the name of the unique id for the service. Usually either `'FID'` or `'OBJECTID'`.</td>
        </tr>
        <tr>
            <td><code>from</code></td>
            <td><code>Date</code></td>
            <td>When paired with <code>to</code> defines the time range of features to display. Requires the Feature Layer to be time enabled.</td>
        </tr>
        <tr>
            <td><code>to</code></td>
            <td><code>Date</code></td>
            <td>When paired with <code>from</code> defines the time range of features to display. Requires the Feature Layer to be time enabled.</td>
        </tr>
        <tr>
            <td><code>timeField</code></td>
            <td><code>false</code></td>
            <td>The name of the field to lookup the time of the feature. Can be an object like <code>{start:'startTime', end:'endTime'}</code> or a string like <code>'created'</code>.</td>
        </tr>
        <tr>
            <td><code>timeFilterMode</code></td>
            <td><code>'server'</code> (default) or <code>'client'</code></td>
            <td>Determines where features are filtered by time. By default features will be filtered by the server. If set to <code>'client'</code> all features are requested and filtered by the app before display.</td>
        </tr>
        <tr>
            <td><code>simplifyFactor</code></td>
            <td><code>Integer</code></td>
            <td>How much to simplify polygons and polylines. More means better performance, and less means more accurate representation.</td>
        </tr>
        <tr>
            <td><code>precision</code></td>
            <td><code>Integer</code></td>
            <td>How many digits of precision to request from the server. <a href="https://en.wikipedia.org/wiki/Decimal_degrees">Wikipedia</a> has a great reference of digit precision to meters.</td>
        </tr>
        <tr>
            <td><code>token</code></td>
            <td><code>String</code></td>
            <td>If you pass a token in your options it will be included in all requests to the service.</td>
        </tr>
        <tr>
            <td><code>proxy</code></td>
            <td><code>String</code></td>
            <td>URL of an <a href="https://developers.arcgis.com/javascript/jshelp/ags_proxy.html">ArcGIS API for JavaScript proxies</a> or <a href="https://github.com/Esri/resource-proxy">ArcGIS Resource Proxies</a> to use for proxying POST requests.</td>
        </tr>
        <tr>
            <td><code>useCors</code></td>
            <td><code>Boolean</code></td>
            <td>If this service should use CORS when making GET requests.</td>
        </tr>
    </tbody>
</table>

`ClusteredFeatureLayer` will also accept any options that can be passed to [Leaflet.MarkerClusterGroup](https://github.com/Leaflet/Leaflet.markercluster#all-options) to customize the behavior and appearance of the clustering.

### Events

| Event | Type | Description |
| --- | --- | --- |
| `loading` | [<`LoadingEvent`>]({{assets}}api-reference/events.html#loading-event) | Fires when new features start loading. |
| `load` | [<`LoadEvent`>]({{assets}}api-reference/events.html#load-event) | Fires when all features in the current bounds of the map have loaded. |
| `createfeature` | [<`CreateFeatureEvent`>]({{assets}}api-reference/events.html#feature-create) | Fired when a feature from the Feature Layer is loaded for the first time. |
| `removefeature` | [<`RemoveFeatureEvent`>]({{assets}}api-reference/events.html#feature-remove) | Fired when a feature on the layer is removed from the map. |
| `addfeature` | [<`AddFeatureEvent`>]({{assets}}api-reference/events.html#feature-add) | Fired when a previously removed feature is added back to the map. |

`L.esri.FeatureLayer` also fires all  [`L.esri.FeatureLayerService`]({{assets}}api-reference/services/feature-layer-service.html) events.

In additon to these events `L.esri.Cluster.FeatureLayer` also fires the following [Mouse Events](https://leafletjs.com/reference.html#event-objects) `click`, `dblclick`, `mouseover`, `mouseout`, `mousemove`, and `contextmenu`, `clusterclick`, `clusterdblclick`, `clustermouseover`, `clustermousemove`, and `clustercontextmenu` as well as the following the [Popup Events](https://leafletjs.com/reference.html#event-objects) `popupopen` and `popupclose`.

### Methods

<table>
    <thead>
        <tr>
            <th>Method</th>
            <th>Returns</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>setStyle({{{param 'PathOptions' 'style' 'https://leafletjs.com/reference.html#path-options'}}})</code><br><br><code>setStyle({{{param 'Function' 'style'}}})</code></td>
            <td><code>this</code></td>
            <td>Sets the given path options to each layer that has a <code>setStyle</code> method. Can also be a <code>Function</code> that will recive a <code>layer</code> argument and should return <a href="https://leafletjs.com/reference.html#path-options">Path Options</a></td>
        </tr>
        <tr>
            <td><code>resetStyle({{{param 'String or Integer' id}}})</code></td>
            <td><code>this</code></td>
            <td>Given the ID of a feature, reset that feature to the original style, useful for resetting style after hover events.</td>
        </tr>
        <tr>
            <td><code>setStyle({{{param 'PathOptions' 'style' 'https://leafletjs.com/reference.html#path-options'}}})</code><br><br><code>setStyle({{{param 'Function' 'style'}}})</code></td>
            <td><code>this</code></td>
            <td>Sets the given path options to each layer that has a <code>setStyle</code> method. Can also be a <code>Function</code> that will receive a <code>feature</code> argument and should return <a href="https://leafletjs.com/reference.html#path-options">Path Options</a>
            <pre><code class="language-javascript">featureLayer.setStyle({
  color: 'white'
})</code></pre>
            <pre><code class="language-javascript">featureLayer.setStyle(1, function(feature){
  return {
    weight: feature.properties.pixelWidth
  };
})</code></pre>
        <tr>
            <td><code>eachFeature({{{param 'Function' 'fn'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>
                Calls the passed function against every feature. The function will be passed the layer that represents the feature.
<pre class="js"><code>featureLayer.eachFeature(function(layer){
  console.log(layer.feature.properties.NAME);
});</code></pre>
            </td>
        </tr>
        <tr>
            <td><code>getFeature({{{param 'String or Integer' id}}} id)</code></td>
            <td><code>Layer</code></td>
            <td>Given the id of a Feature return the layer on the map that represents it. This will usually be a Leaflet vector layer like <a href="https://leafletjs.com/reference.html#polyline">Polygon</a> or <a href="https://leafletjs.com/reference.html#polyline">Polygon</a>, or a Leaflet <a href="https://leafletjs.com/reference.html#marker">Marker</a>.</td>
        </tr>
        <tr>
            <td><code>getWhere()</code></td>
            <td><code>String</code></td>
            <td>Returns the current `where` setting</td>
        </tr>
        <tr>
            <td><code>setWhere({{{param 'String' 'where'}}}, {{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>Sets the new `where` option and refreshes the layer to reflect the new <code>where</code> filter. Accepts an optional callback and function context.</td>
        </tr>
        <tr>
            <td><code>getTimeRange()</code></td>
            <td><code>Array</code></td>
            <td>Returns the current time range as an array like <code>[from, to]</code></td>
        </tr>
        <tr>
            <td><code>setTimeRange({{{param 'Date' 'from'}}}, {{{param 'Date' 'to'}}}, , {{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>Sets the current time filter applied to features. An optional callback is run upon completion if <code>timeFilterMode</code> is set to <code>'server'</code>. Also accepts function context as the last argument.</td>
        </tr>
        <tr>
            <td><code>authenticate({{{param 'String' 'token'}}})</code></td>
            <td><code>this</code></td>
            <td>Authenticates this service with a new token and runs any pending requests that required a token.</td>
        </tr>
        <tr>
            <td><code>query()</code></td>
            <td><code>this</code></td>
            <td>
                Returns a new <a href="../tasks/query.html"><code>L.esri.Query</code></a> object that can be used to query this layer. Your callback function will be passed a <a href="https://tools.ietf.org/html/rfc7946#section-3.3">GeoJSON FeatureCollection</a> with the results or an error.
<pre class="js"><code>featureLayer.query()
            .within(latlngbounds)
            .where("Direction = 'WEST'")
            .run(function(error, featureCollection){
                console.log(featureCollection);
            });</code></pre>
            </td>
        </tr>
        <tr>
            <td><code>metadata({{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>
                Requests metadata about this Feature Layer. Callback will be called with `error` and `metadata`.
<pre class="js"><code>featureLayer.metadata(function(error, metadata){
  console.log(metadata);
});</code></pre>
            </td>
        </tr>
 <tr>
            <td><code>addFeature({{{param 'GeoJSON Feature' 'feature' 'https://tools.ietf.org/html/rfc7946#section-3.2'}}}, {{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>
                Adds a new feature to the feature layer. this also adds the feature to the map if creation is successful.
                <ul>
                    <li>Requires authentication as a user who has permission to edit the service in ArcGIS Online or the user who created the service.</li>
                    <li>Requires the <code>Create</code> capability be enabled on the service. You can check if creation exists by checking the metadata of your service under capabilities in the metadata.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>updateFeature({{{param 'GeoJSON Feature' 'feature' 'https://tools.ietf.org/html/rfc7946#section-3.2'}}}, {{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>
                Update the provided feature on the Feature Layer. This also updates the feature on the map.
                <ul>
                    <li>Requires authentication as a user who has permission to edit the service in ArcGIS Online or the user who created the service.</li>
                    <li>Requires the <code>Update</code> capability be enabled on the service. You can check if creation exists by checking the metadata of your service under capabilities in the metadata.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>deleteFeature({{{param 'String or Integer' 'id'}}}, {{{param 'Function' 'callback'}}}, {{{param 'Object' 'context'}}})</code></td>
            <td><code>this</code></td>
            <td>
                Remove the feature with the provided id from the feature layer. This will also remove the feature from the map if it exists.
                <ul>
                    <li>Requires authentication as a user who has permission to edit the service in ArcGIS Online or the user who created the service.</li>
                    <li>Requires the <code>Update</code> capability be enabled on the service. You can check if creation exists by checking the metadata of your service under capabilities in the metadata.</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Example

Live sample [here](https://esri.github.io/esri-leaflet/examples/clustering-feature-layers.html).

```xml
<link rel="stylesheet" type="text/css" href="./MarkerCluster.Default.css">
<link rel="stylesheet" type="text/css" href="./MarkerCluster.css">
<script src="./leaflet.markercluster.js"></script>
<script>./esri-leaflet-cluster.js</script>
```

```js
var map = L.map('map').setView([45.53, -122.64], 16);
L.esri.basemapLayer('Streets').addTo(map);

var url = 'https://services.arcgis.com/rOo16HdIMeOBI4Mb/arcgis/rest/services/stops/FeatureServer/0';

L.esri.Cluster.featureLayer({
  url: url,
  // Cluster Options
  polygonOptions: {
    color: '#2d84c8'
  },
  // Feature Layer Options
  pointToLayer: function (geojson, latlng) {
    return L.circleMarker(latlng, 10, {
      color: '#2D84C8'
    });
  }
}).addTo(map);
```
