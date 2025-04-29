<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TAMU Parking Lots Map</title>

  <!-- ArcGIS CSS -->
  <link rel="stylesheet" href="https://js.arcgis.com/4.6/esri/css/main.css" />

  <!-- Internal CSS -->
  <style>
    html, body, #viewDiv {
      height: 100%;
      margin: 0;
      padding: 0;
      font-family: sans-serif;
    }
    #viewDiv {
      position: absolute;
      top: 0;
      bottom: 0;
      right: 0;
      left: 0;
    }
  </style>

  <!-- ArcGIS JS API -->
  <script src="https://js.arcgis.com/4.6/"></script>
</head>

<body>
  <div id="viewDiv"></div>

  <script>
    require([
      "esri/Map",
      "esri/views/MapView",
      "esri/layers/FeatureLayer",
      "dojo/domReady!"
    ], function(Map, MapView, FeatureLayer) {

      // Create the map
      var map = new Map({
        basemap: "streets"
      });

      // Create the view centered on TAMU
      var view = new MapView({
        container: "viewDiv",
        map: map,
        center: [-96.339469, 30.617492],
        zoom: 16
      });

      // Parking Lots Feature Layer with popup
      var parkingLotsLayer = new FeatureLayer({
        portalItem: {
          id: "22fa00325613411081c8f1706e17c6cc"
        },
        popupTemplate: {
          title: "{Name}",  // Display the Name of the parking lot (e.g., "Fan Field")
          content: [{
            type: "fields",
            fieldInfos: [
              {
                fieldName: "Name",
                label: "Parking Lot Name",
                visible: true
              },
              {
                fieldName: "LotName",
                label: "Lot Description",
                visible: true
              },
              {
                fieldName: "LotType",
                label: "Lot Type",
                visible: true
              },
              {
                fieldName: "Shape__Area",
                label: "Area (sq. ft.)",
                visible: true
              },
              {
                fieldName: "Shape__Length",
                label: "Length (m)",
                visible: true
              }
            ]
          }]
        }
      });

      // Add the parking lots layer to the map
      map.add(parkingLotsLayer);
    });
  </script>
</body>
</html>
