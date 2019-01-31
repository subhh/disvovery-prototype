# New facet types for typo3-find extension of subugoe

## Basic architecture

These extensions offer new facets for [typo3-find extension](https://github.com/subugoe/typo3-find). 

## Common usage
### Installing extension
You can install via extension manager or with composer.
### Adding static templates
In web backend you have to add the static template.

## List of facets

### hos-t3find-facet-heatmap

![](https://i.imgur.com/RH0oepr.png)

#### Typoscript:
```
plugin.tx_find.settings.facets.20 {
   type = Heatmap
   fetchMaximum = 1000
   field = geoLocationPoint 
   tileProvider = provider=stamen&type=toner-lite&tile={z}/{x}/{y}{r}
   attribution = Map tiles by <a title="Design by Stamen Design" href="https://stamen.com/maps/">Stamen Design</a>, CC BY 3.0
```

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
