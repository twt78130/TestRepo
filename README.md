# OpenStreetMap Sample for WinForms
OpenStreetMap (OSM) is a collaborative project to create free geographic data for the entire world. It can be thought of as a "Free Wiki World Map. 
Now the latest version of MapSuite can support that. 

![Screenshot](https://github.com/thinkgeogithub/TestRepo/blob/master/friendsnetwork.png)

### Requirements
This sample requires the **MapSuite 10.0.0.0** (or later) development build.

## About the Code

###The preceeding code is added to the load event for your application.

The first step is to set `winformsMap.MapUnit` to `GeographyUnit.Meters`. 
You'll then be able to add the OpenStreetMap overlay with the following code:
```csharp
OpenStreetMapOverlay osmOvelerlay = new OpenStreetMapOverlay();
winformsMap.Overlays.Add(osmOvelerlay);
```
Once the overlay is added, be sure to call `winformsMap.Refresh()` to get the map to draw the new layer. 

### Getting Help

[Map Suite Desktop for Winforms Wiki Resources](http://wiki.thinkgeo.com/wiki/map_suite_desktop_edition)

[Map Suite Desktop for Winforms Product Description](http://thinkgeo.com/map-suite-developer-gis/desktop-edition/)

### Key APIs
This example makes use of the following APIs:

[ThinkGeo.MapSuite.Layers.OpenStreetMaps](http://wiki.thinkgeo.com/wiki/thinkgeo.mapsuite.core.openstreetmaplayer)


### About ThinkGeo
ThinkGeo is a GIS (Geographic Information Systems) company founded in 2004 and located in Frisco, TX. Our clients are in more than 40 industries including agriculture, energy, transportation, government, engineering, software development, and defense.




