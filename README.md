# How extends find extension

## Basic architecture

This extension offers new facets for [typo3-find extension](https://github.com/subugoe/typo3-find). 
The working name of this extension is `discovery`.

## Prerequisites

This snippet below extends the search path. Our new path is the first in the search order:
```
plugin.tx_find {
   view {
        partialRootPaths {
            20 = typo3conf/ext/discovery/Resources/Private/Partials/
        }
  }
}
```

## Facets

In original extension a couple of facet rendering pattern are available. For extending and creating new ones new partials will need. In this partials all parameters are realised with HTML5 data HTML entities. This pattern avoids Javascript inside the HTML code. The partials build a "bridge" between Typoscript and Javascript namespace.

### Heatmap

Example for typoscript:
```
plugin.tx_find.settings.facets.20 {
   type = Heatmap
   fetchMaximum = 1000
   field = geoLocationPoint 
   tileProvider = provider=stamen&type=toner-lite&tile={z}/{x}/{y}{r}
   attribution = Map tiles by <a title="Design by Stamen Design" href="https://stamen.com/maps/">Stamen Design</a>, CC BY 3.0
```

### ThreeStateSwitch
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

