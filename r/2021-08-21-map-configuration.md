---
description: How to configure and style base maps for Choropleths and Bubble Maps.
display_as: maps
language: r
layout: base
name: Map Configuration and Styling
order: 12
output:
  html_document:
    keep_md: true
page_type: u-guide
permalink: r/map-configuration/
thumbnail: thumbnail/county-level-choropleth.jpg
---




### Mapbox Maps vs Geo Maps

Plotly supports two different kinds of maps:

1. **Mapbox maps** are [tile-based maps](https://en.wikipedia.org/wiki/Tiled_web_map). If your figure is created with one or more traces of type `Scattermapbox`, `Choroplethmapbox` or `Densitymapbox`, the `layout$mapbox` object in your figure contains configuration information for the map itself.
2. **Geo maps** are outline-based maps. If your figure is created with a `scattergeo` or `choropleth` function, the `layout$geo` object in your figure contains configuration information for the map itself.

This page documents Geo outline-based maps, and the [Mapbox Layers documentation](https://plotly.com/r/mapbox-layers/) describes how to configure Mapbox tile-based maps.

**Note:** Every configuration option here is equally applicable to non-empty maps created with the Plotly  `scattergeo` and `choropleth` functions.

### Physical Base Maps

Plotly Geo maps have a built-in base map layer composed of "physical" and "cultural" (i.e. administrative border) data from the [Natural Earth Dataset](https://www.naturalearthdata.com/downloads/). Various lines and area fills can be shown or hidden, and their color and line-widths specified. In the default `plotly` template, a map frame and physical features such as a coastal outline and filled land areas are shown, at a small-scale 1:110m resolution:


```r
library(plotly)
g <- list(showland = TRUE,
  landcolor = toRGB("#e5ecf6"))
fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-f76452d0803a9d77e1ad" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-f76452d0803a9d77e1ad">{"x":{"visdat":{"31b5f4904fa":["function () ","plotlyVisDat"]},"cur_data":"31b5f4904fa","attrs":{"31b5f4904fa":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

Here is a map with all physical features enabled and styled, at a larger-scale 1:50m resolution:


```r
library(plotly)

g <- list(
  scope = 'world',
  showland = TRUE,
  landcolor = toRGB("LightGreen"),
  showocean = TRUE,
  oceancolor = toRGB("LightBlue"),
  showlakes = TRUE,
  lakecolor = toRGB("Blue"),
  showrivers = TRUE,
  rivercolor = toRGB("Blue"),
  resolution = 50,
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-23626e6aa415dfdb477d" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-23626e6aa415dfdb477d">{"x":{"visdat":{"31b54104eaed":["function () ","plotlyVisDat"]},"cur_data":"31b54104eaed","attrs":{"31b54104eaed":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"scope":"world","showland":true,"landcolor":"rgba(144,238,144,1)","showocean":true,"oceancolor":"rgba(173,216,230,1)","showlakes":true,"lakecolor":"rgba(0,0,255,1)","showrivers":true,"rivercolor":"rgba(0,0,255,1)","resolution":50,"showland.1":true,"landcolor.1":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Disabling Base Maps

In certain cases, such as large scale [choropleth maps](plotly.com/r/choropleth-maps/), the default physical map can be distracting. In this case the `layout$geo$visible` attribute can be set to `FALSE` to hide all base map attributes except those which are explicitly set to true. For example in the following map we hide all physical features except rivers and lakes, neither of which are shown by default:


```r
library(plotly)

g <- list(
  scope = 'world',
  visible = F,
  showlakes = TRUE,
  lakecolor = toRGB("Blue"),
  showrivers = TRUE,
  rivercolor = toRGB("Blue"),
  resolution = 50
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-49dabc11229997071cb5" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-49dabc11229997071cb5">{"x":{"visdat":{"31b524b5fa6e":["function () ","plotlyVisDat"]},"cur_data":"31b524b5fa6e","attrs":{"31b524b5fa6e":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"scope":"world","visible":false,"showlakes":true,"lakecolor":"rgba(0,0,255,1)","showrivers":true,"rivercolor":"rgba(0,0,255,1)","resolution":50},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Cultural Base Maps

In addition to physical base map features, a "cultural" base map is included which is composed of country borders and selected sub-country borders such as states.

**Note and disclaimer:** cultural features are by definition subject to change, debate and dispute. Plotly includes data from Natural Earth "as-is" and defers to the [Natural Earth policy regarding disputed borders](https://www.naturalearthdata.com/downloads/50m-cultural-vectors/50m-admin-0-countries-2/) which read:

> Natural Earth Vector draws boundaries of countries according to defacto status. We show who actually controls the situation on the ground.

**To create a map with your own cultural features** please refer to our [choropleth documentation](plotly.com/r/choropleth-maps/).

Here is a map with only cultural features enabled and styled, at a 1:50m resolution, which includes only country boundaries. See below for country sub-unit cultural base map features:


```r
library(plotly)

g <- list(
  scope = 'world',
  visible = F,
  showcountries = T,
  countrycolor = toRGB("Purple"),
  resolution = 50,
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-f547300770ce5c13d824" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-f547300770ce5c13d824">{"x":{"visdat":{"31b51e6f8855":["function () ","plotlyVisDat"]},"cur_data":"31b51e6f8855","attrs":{"31b51e6f8855":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"scope":"world","visible":false,"showcountries":true,"countrycolor":"rgba(160,32,240,1)","resolution":50,"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Map Projections

Geo maps are drawn according to a given map [projection](https://en.wikipedia.org/wiki/Map_projection) that flattens the Earth's roughly-spherical surface into a 2-dimensional space.

The available projections are `'equirectangular'`, `'mercator'`, `'orthographic'`, `'natural earth'`, `'kavrayskiy7'`, `'miller'`, `'robinson'`, `'eckert4'`, `'azimuthal equal area'`, `'azimuthal equidistant'`, `'conic equal area'`, `'conic conformal'`, `'conic equidistant'`, `'gnomonic'`, `'stereographic'`, `'mollweide'`, `'hammer'`, `'transverse mercator'`, `'albers usa'`, `'winkel tripel'`, `'aitoff'` and `'sinusoidal'`.


```r
library(plotly)

g <- list(
  projection = list(
    type = 'orthographic'
  ),
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-0043698b69d6b11563f4" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-0043698b69d6b11563f4">{"x":{"visdat":{"31b552c07a30":["function () ","plotlyVisDat"]},"cur_data":"31b552c07a30","attrs":{"31b552c07a30":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"projection":{"type":"orthographic"},"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>


```r
library(plotly)

g <- list(
  projection = list(
    type = 'natural earth'
  ),
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-0b111492e845d4e8cb5f" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-0b111492e845d4e8cb5f">{"x":{"visdat":{"31b51a76a173":["function () ","plotlyVisDat"]},"cur_data":"31b51a76a173","attrs":{"31b51a76a173":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"projection":{"type":"natural earth"},"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

Map projections can be rotated using the `layout$geo$projection$rotation` attribute, and maps can be translated using the `layout$geo$center` attributed, as well as truncated to a certain longitude and latitude range using the `layout$geo$lataxis$range` and `layout$geo$lonaxis$range`.

The map below uses all of these attributes to demonstrate the types of effect this can yield:


```r
library(plotly)

g <- list(
  projection = list(
    rotation = list(lon=30, lat=30, roll=30)
  ),
  center = list(lon=-30, lat=-30),
  lonaxis = list(range = c(0, 200)),
  lataxis = list(range = c(-50,20)),showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-55870118ff9864b9f724" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-55870118ff9864b9f724">{"x":{"visdat":{"31b521a897b6":["function () ","plotlyVisDat"]},"cur_data":"31b521a897b6","attrs":{"31b521a897b6":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"projection":{"rotation":{"lon":30,"lat":30,"roll":30}},"center":{"lon":-30,"lat":-30},"lonaxis":{"range":[0,200]},"lataxis":{"range":[-50,20]},"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Automatic Zooming or Bounds Fitting

The `layout$geo$fitbounds` attribute can be set to `locations` to automatically set the center and latitude and longitude range according to the data being plotted. See the [choropleth maps](https://plotly.com/r/choropleth-maps/) documentation for more information.


```r
library(plotly)

g <- list(
  fitbounds = "locations",
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'lines', lat = list(0,15,20,35), lon = list(5,10,25,30))
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-d2d20f45cc3b3f598db2" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-d2d20f45cc3b3f598db2">{"x":{"visdat":{"31b523db130f":["function () ","plotlyVisDat"]},"cur_data":"31b523db130f","attrs":{"31b523db130f":{"mode":"lines","lat":[0,15,20,35],"lon":[5,10,25,30],"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"fitbounds":"locations","showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"lines","lat":[0,15,20,35],"lon":[5,10,25,30],"type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Named Map Scopes and Country Sub-Units

In addition, the named "scope" of a map defines a sub-set of the earth's surface to draw. Each scope has a _default projection type, center and roll, as well as bounds_, and certain scopes contain country sub-unit cultural layers certain resolutions, such as `scope="north america"` at `resolution=50` which contains US state and Canadian province boundaries.

The available scopes are: `'world'`, `'usa'`, `'europe'`, `'asia'`, `'africa'`, `'north america'`, `'south america'`.


```r
library(plotly)

g <- list(
  visible = F,
  resolution = 50,
  scope = "north america",
  showcountries = T,
  countrycolor = toRGB("Black"),
  showsubunits = T,
  subunitcolor = toRGB("Blue"),
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-2d0ba4ca03a58d38977e" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-2d0ba4ca03a58d38977e">{"x":{"visdat":{"31b529d978aa":["function () ","plotlyVisDat"]},"cur_data":"31b529d978aa","attrs":{"31b529d978aa":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"visible":false,"resolution":50,"scope":"north america","showcountries":true,"countrycolor":"rgba(0,0,0,1)","showsubunits":true,"subunitcolor":"rgba(0,0,255,1)","showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

The `"usa"` scope contains state boundaries at both resolutions, and uses the special `'albers usa'` projection which moves Alaska and Hawaii closer to the "lower 48 states" to reduce projection distortion and produce a more compact map.


```r
library(plotly)

g <- list(
  visible = F,
  resolution = 110,
  scope = "usa",
  showcountries = T,
  countrycolor = toRGB("Black"),
  showsubunits = T,
  subunitcolor = toRGB("Blue"),
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-01f90d8d12dde9ab7046" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-01f90d8d12dde9ab7046">{"x":{"visdat":{"31b5668adb":["function () ","plotlyVisDat"]},"cur_data":"31b5668adb","attrs":{"31b5668adb":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"visible":false,"resolution":110,"scope":"usa","showcountries":true,"countrycolor":"rgba(0,0,0,1)","showsubunits":true,"subunitcolor":"rgba(0,0,255,1)","showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Graticules (Latitude and Longitude Grid Lines)

A graticule can be drawn using `layout$geo$lataxis$showgrid` and `layout$geo$lonaxis$showgrid` with options similar to [2d cartesian ticks](https://plotly.com/r/axes/).


```r
library(plotly)

g <- list(
  lonaxis = list(showgrid = T),
  lataxis = list(showgrid = T),
  showland = TRUE,
  landcolor = toRGB("#e5ecf6")
)

fig <- plot_ly(type = 'scattergeo', mode = 'markers')
fig <- fig %>% layout(geo = g)
fig
```

<div id="htmlwidget-51e3bfa9e2f28c5ddca4" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-51e3bfa9e2f28c5ddca4">{"x":{"visdat":{"31b5827ccc7":["function () ","plotlyVisDat"]},"cur_data":"31b5827ccc7","attrs":{"31b5827ccc7":{"mode":"markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scattergeo"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"geo":{"lonaxis":{"showgrid":true},"lataxis":{"showgrid":true},"showland":true,"landcolor":"rgba(229,236,246,1)"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"mode":"markers","type":"scattergeo","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

### Reference

See https://plotly.com/r/reference/layout/geo/ for more information and chart attribute options!

### What About Dash?

[Dash for R](https://dashr.plot.ly/) is an open-source framework for building analytical applications, with no Javascript required, and it is tightly integrated with the Plotly graphing library. 

Learn about how to install Dash for R at https://dashr.plot.ly/installation.

Everywhere in this page that you see `fig`, you can display the same figure in a Dash for R application by passing it to the `figure` argument of the [`Graph` component](https://dashr.plot.ly/dash-core-components/graph) from the built-in `dashCoreComponents` package like this:


```r
library(plotly)

fig <- plot_ly() 
# fig <- fig %>% add_trace( ... )
# fig <- fig %>% layout( ... ) 

library(dash)
library(dashCoreComponents)
library(dashHtmlComponents)

app <- Dash$new()
app$layout(
    htmlDiv(
        list(
            dccGraph(figure=fig) 
        )
     )
)

app$run_server(debug=TRUE, dev_tools_hot_reload=FALSE)
```
