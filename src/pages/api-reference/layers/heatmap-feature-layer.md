---
title: L.esri.Heat.FeatureLayer
layout: documentation.hbs
---

# {{page.data.title}}

Extends [`L.esri.Layers.FeatureLayer`]({{assets}}api-reference/layers-feature-layer.html)

`L.esri.Heat.FeatureLayer` provides integration for Feature Layers with the [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) plugin. Because of the extra dependency on Leaflet.heat we do not include `L.esri.Heat.FeatureLayer` in the default build of Esri Leaflet. You will need to include your own copy of the [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) plugin in your application as well.

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
            <td><code class="nobr">L.esri.Heat.featureLayer({{{param 'Object' 'options'}}})</code></td>
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
            <td><code>precision</code></td>
            <td><code>Integer</code></td>
            <td>How many digits of geometry precision to request from the server. <a href="https://en.wikipedia.org/wiki/Decimal_degrees">Wikipedia</a> has a great reference of digit precision to meters.</td>
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

`L.esri.Heat.FeatureLayer` will also accept any options that can be passed to [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat#lheatlayerlatlngs-options) to customize the appearance of the heatmap.

### Events

| Event | Type | Description |
| --- | --- | --- |
| `loading` | [&lt;LoadingEvent&gt;]() | Fires when new features start loading. |
| `load` | [&lt;Load&gt;]() | Fires when all features in the current bounds of the map have loaded. |

`L.esri.Heat.FeatureLayer` also fires all  [`L.esri.FeatureLayerService`]({{assets}}api-reference/services/feature-layer-service.html) events.

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

Live sample [here](https://esri.github.io/esri-leaflet/examples/visualize-points-as-a-heatmap.html).

```xml
<script src="./leaflet-heat.js"></script>
<script src="./esri-leaflet-heatmap.js"></script>
```

```js
var map = new L.Map('map').setView([40.722868115037, -73.92142295837404], 14);

L.esri.basemapLayer('Gray').addTo(map);

L.esri.Heat.featureLayer({
  url: 'https://services.arcgis.com/rOo16HdIMeOBI4Mb/arcgis/rest/services/Graffiti_Locations3/FeatureServer/0',
  radius: 12
}).addTo(map);
```
