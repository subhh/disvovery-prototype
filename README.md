# New facet types for typo3-find extension of subugoe

## Basic architecture

These extensions offer new facets views for [typo3-find extension](https://github.com/subugoe/typo3-find). 

## Example implementation

On [HamburgOpenScience](https://openscience.hamburg.de/) you can see an example implementation.

## Common usage
### Installing extension
You can install via extension manager or with composer.

![](https://i.imgur.com/KnVPPZX.png)

### Adding core static templates
For all facet view you have to add this static template:

![](https://i.imgur.com/ShSRgs2.png)

## List of facets

### Heatmap vie

Example rendering:

![](https://i.imgur.com/RH0oepr.png)

#### Typoscript:

First add static template from extension:
![](https://i.imgur.com/70D5dCS.png)

Now you can add new type inside `plugin.tx_find.settings` section of typoscript: 
```
plugin.tx_find.settings.facets.heatmap {
   type = Heatmap
   fetchMaximum = 1000
   field = geoLocationPoint 
   tileProvider = https://stamen-tiles-c.a.ssl.fastly.net/toner-lite/{z}/{x}/{y}@2x.png
   attribution = Map tiles by <a title="Design by Stamen Design" href="https://stamen.com/maps/">Stamen Design</a>, CC BY 3.0
```
#### Other maps types

On [this page](https://leaflet-extras.github.io/leaflet-providers/preview/) you can choose an other map provider.

#### General Data Protection Regulation (EUDSVGO)
If you want avoid access of not local web servers you can use the embedded tile cache. Additional the class caches the tiles. This avoid to much traffic of native tile provider. Attention: maybe it is a good idea to limit the range.

```
plugin.tx_find.settings.facets.20.tileProvider = ?eID=tile&url=ORIGINAL_URL
```
You have to encode the url.In the example above `https%3A%2F%2Fstamen-tiles-a.a.ssl.fastly.net%2Ftoner-lite%2F%7Bz%7D%2F%7Bx%7D%2F%7By%7D%402x.png`

### hos-t3find-facet-threestateswitch

![](https://i.imgur.com/nZOk1ft.png)

#### Typescript configuration:

For configuration add these properties below to the section:
```
plugin.tx_find.settings.facets.10 {
       id = OpenAccess
       headerhidden = 1
       field = rightsOA
       type = Threestateswitch
       displayDefault = 2
       link = ?tx_find_find[facet][OpenAccess][%s]=1&tx_find_find[controller]=Search
       csspath= typo3conf/ext/discovery/Resources/Public/CSS/toggle-switch.css
       toast = Publikationen vom Typ: „%s“
       query=(rightsOA:%s)
       values {
              Open=Open Access
              All=Open Access,zugriffsbeschränkt
              Close=zugriffsbeschränkt
       }
       labels {
              Open=Open Access
              All=Alle Dokumente
              Close=Restricted Access 
       }
}
```
### hos-t3find-facet-pie

![](https://i.imgur.com/vejQE2M.png)

### hos-t3find-facet-wordcloud

![](https://i.imgur.com/g2FVhXE.png)

### hos-t3find-facet-ddc
![](https://i.imgur.com/7yyQNYf.png)
