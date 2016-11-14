# Label Point with Circle Symbol and Mask Description
This sample demonstrates how you can create a friends network using geolocations. It uses a combination of styles and labeling allowing you to show points and distances between friends.

![Screenshot](https://github.com/thinkgeogithub/TestRepo/blob/master/friendsnetwork.png)

## Sample Code
Create the base map overlay to use for your application.
```csharp
// Create WorldMapKitWmsWpfOverlay as the basemap.
            WorldMapKitWmsWpfOverlay wmk = new WorldMapKitWmsWpfOverlay();
            wmk.Projection = WorldMapKitProjection.SphericalMercator;
            wpfMap1.Overlays.Add(wmk);
```

You'll then create a single tile overlay for your data -- 
```csharp
 LayerOverlay layerOverlay = new LayerOverlay();
            layerOverlay.TileType = TileType.SingleTile;
            wpfMap1.Overlays.Add("layerOverlay", layerOverlay);
 
            // Create the size of point circle.
            int symbolSize = 50;
```



