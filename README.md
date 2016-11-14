# OpenStreetMap Sample for WinForms
OpenStreetMap (OSM) is a collaborative project to create free geographic data for the entire world. It can be thought of as a "Free Wiki World Map. 
Now the latest version of MapSuite can support that. 

### Requirements
This sample requires the **MapSuite 10.0.0.0** (or later) development build.


![Screenshot](https://github.com/thinkgeogithub/TestRepo/blob/master/friendsnetwork.png)

## Sample Code

###The preceeding code is added to the load event for your application.

The first step is to set `winformsMap.MapUnit` to `GeographyUnit.Meters`. 
You'll then be able to add the OpenStreetMap overlay with the following code:
```csharp
OpenStreetMapOverlay osmOvelerlay = new OpenStreetMapOverlay();
winformsMap.Overlays.Add(osmOvelerlay);
```
Once the overlay is added, be sure to call `winformsMap.Refresh()` to get the map to draw the new layer. 






