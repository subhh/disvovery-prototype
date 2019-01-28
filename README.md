# How extends find extension

## Basic architecture

All modifications of extension are realised in a new extension named `discovery`. 

### Facets

In original extension a couple of facet rendering pattern are available. For extending and creating new ones new partials will need. In this partials all parameters are realised with HTML5 data HTML entities. This pattern avoids Javascript inside the HTML code. The partials build a "bridge" between Typoscript and Javascript namespace.

#### Heatmap

Example for typoscript:
```
plugin.tx_find.settings.facets.20 {
   type = Heatmap
   fetchMaximum = 1000
   field = geoLocationPoint 
   tileProvider = ?eID=tile&provider=stamen&type=toner-lite&tile={z}/{x}/{y}{r}
   attribution = Map tiles by <a title="Design by Stamen Design" href="https://stamen.com/maps/">Stamen Design</a>, CC BY 3.0
```
This snippets tells the extension to look for `geolocationPoint` of solr and and to use some properties.

Content of ``/discovery/Resources/Private/Partials/Facets/Facet/Heatmap.html`:

```
<div class="facetMap-container">
  <div id="schaufenster_heatmap" class="heatmapContainer"
        data-facetdata="{f:format.json(value:facetData.values)}"
        data-fetchmaximum="{facetInfo.fetchMaximum}" 
        data-tileprovider="{facetInfo.tileProvider}"
        data-attribution="{facetInfo.attribution}"
  </div>
</div>
```
`facetData` comes from controler (solr response data) and `facetInfo`comes from TS.

This partial generated a snippet like this:

```
<div class="facetMap-container">
  <div id="schaufenster_heatmap" class="heatmapContainer"
        data-facetdata="{&quot;53.4635384,9.9674,17&quot;:26}"
        data-fetchmaximum="1000" 
        data-tileprovider="?eID=tile&amp;provider=stamen">
  </div>
</div>
```
