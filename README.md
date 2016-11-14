# OpenStreetMap Sample for WinForms
OpenStreetMap (OSM) is a collaborative project to create free geographic data for the entire world. It can be thought of as a "Free Wiki World Map. 
Now the latest version of MapSuite can support that. 

### Requirements
This sample requires the 10.0.0.0 (or later) development build.


![Screenshot](https://github.com/thinkgeogithub/TestRepo/blob/master/friendsnetwork.png)

## Sample Code

###The preceeding code is added to the load event for your application.

The first step is to set `winformsMap.MapUnit` to `GeographyUnit.Meters`. 
You'll then be able to add the OpenStreetMap overlay with the following code:
```csharp
OpenStreetMapOverlay osmOvelerlay = new OpenStreetMapOverlay();
winformsMap.Overlays.Add(osmOvelerlay);
```

You'll then create a single tile overlay for your data and the circle to represent your area. -- 
```csharp
LayerOverlay layerOverlay = new LayerOverlay();
layerOverlay.TileType = TileType.SingleTile;
wpfMap1.Overlays.Add("layerOverlay", layerOverlay);
 
// Create the size of point circle.
int symbolSize = 50;
```

The various styles are used to display your friends in relationship to yourself (represented by the **protagonist**)
```csharp
 // Create the point style for friends
PointStyle friendsPointStyle = new PointStyle(PointSymbolType.Circle, new GeoSolidBrush(new GeoColor(80, GeoColors.Highlight)), new GeoPen(GeoColors.Blue, 1), symbolSize - 15);

// Create the point style for protagonist
PointStyle protagonistPointStyle = new PointStyle(PointSymbolType.Circle, new GeoSolidBrush(new GeoColor(80, GeoColors.DarkOrange)), new GeoPen(GeoColors.DarkOrange, 1), symbolSize);
 
// Create the ValueStyle for PointStyle.
ValueStyle pointValueStyle = new ValueStyle();
pointValueStyle.ColumnName = "role";
pointValueStyle.ValueItems.Add(new ValueItem("friend", friendsPointStyle));
pointValueStyle.ValueItems.Add(new ValueItem("protagonist", protagonistPointStyle));
 
// Create the text style for friendsPointStyle
TextStyle friendsTexStyle = new TextStyle("Name", new GeoFont("Arail", 9, DrawingFontStyles.Bold), new GeoSolidBrush(GeoColor.SimpleColors.Black));

friendsTexStyle.PointPlacement = PointPlacement.Center;
friendsTexStyle.OverlappingRule = LabelOverlappingRule.AllowOverlapping;
 
// Create the text style for protagonist
TextStyle protagonistTextStyle = new TextStyle("Name", new GeoFont("Arail", 9, DrawingFontStyles.Bold), new GeoSolidBrush(GeoColor.SimpleColors.Black));

protagonistTextStyle.PointPlacement = PointPlacement.Center;
protagonistTextStyle.OverlappingRule = LabelOverlappingRule.AllowOverlapping;
 
// Create the ValueStyle for TextStyle.
ValueStyle textValueStyle = new ValueStyle();
textValueStyle.ColumnName = "role";
textValueStyle.ValueItems.Add(new ValueItem("friend", friendsTexStyle));
textValueStyle.ValueItems.Add(new ValueItem("protagonist", protagonistTextStyle));
 
// Create the layer
ShapeFileFeatureLayer friendsLayer = new ShapeFileFeatureLayer(@"..\..\App_Data\friends.shp");
friendsLayer.ZoomLevelSet.ZoomLevel01.CustomStyles.Add(pointValueStyle);
friendsLayer.ZoomLevelSet.ZoomLevel01.CustomStyles.Add(textValueStyle);
friendsLayer.ZoomLevelSet.ZoomLevel01.ApplyUntilZoomLevel = ApplyUntilZoomLevel.Level20;
friendsLayer.Open();
var allFeature = friendsLayer.FeatureSource.GetAllFeatures(ReturningColumnsType.AllColumns);
 
var protagonistPionts = allFeature.Where(f => f.ColumnValues["role"] == "protagonist").ToList();
var friendPionts = allFeature.Where(f => f.ColumnValues["role"] == "friend").ToList();
if (protagonistPionts.Count > 0)
{
    Feature targetFeature = protagonistPionts[0];
    InMemoryFeatureLayer lineLayer = GetTheLineAndRangeLayer(targetFeature, friendPionts);
    layerOverlay.Layers.Add(lineLayer);
}
 
layerOverlay.Layers.Add(friendsLayer);
 
// Set the map extent
wpfMap1.CurrentExtent = new RectangleShape(-10773348.4056994, 3921495.52062368, -10763946.6747371, 3914224.46649529);
wpfMap1.Refresh();




