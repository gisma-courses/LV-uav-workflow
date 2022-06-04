---
title: "Case Study 'Gisselberger Spannweite'"
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-15
morea_summary: Case Study *Gisselberger Spannweite*
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - casestudy

---
# Case Study 'Gisselberger Spannweite'

A case study is conducted using the Gisselberger Spannweite as an example. The goal is the monitoring of the REnaturation measure with the help of sufficiently precise ortho images with low cost drones < 250 grams weight. For this purpose, the DJI Mini 2 is suitable due to the camera quality and the technology of collision-free straight and descent flight.

The planning was created using` QGroundcontrol` while respecting the protection zones as derived from `Airmap` and converted to `Litchi Mission Hub` using the `R` package `uavRmp`. Due to the challenging wind conditions, two intermediate landings for battery replacement were necessary. On-site acquisition, including set-up and tear-down, took roughly 1 hour. 

## Results 

Below you see the result of the *Gisselberger Spannweite* case study. The original resolution of 1.5 cm has been resampled to 5 cm due to data reduction. 
The flight was performed with a DJI Mavic Mini 2. Flight altitude longitudinal flight 70 meters AGL, flight altitude cross flight 50 meters AGL. In Metashape, the default workwlow was selected from `Workflow+->Best Practice->Ortho-no-GPS`. 
<br>
<br>`
  <!-- Include the CesiumJS JavaScript and CSS files -->
  <script src="https://cesium.com/downloads/cesiumjs/releases/1.94/Build/Cesium/Cesium.js"></script>
  <link href="https://cesium.com/downloads/cesiumjs/releases/1.94/Build/Cesium/Widgets/widgets.css" rel="stylesheet">


  <div id="cesiumContainer" ></div>

  <script>
    Cesium.Ion.defaultAccessToken ='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI0M2ViYjgxYi00M2YzLTQ4YjktOTk3NS1iMmQ5MTk2NjllMDgiLCJpZCI6OTYyNDQsImlhdCI6MTY1NDM1NjIyM30.qRSJjdQBu8tWhq6TzyzZnI7k1N4Wg9WehpSIzOKrxjg';

var west = 8.7476979731805926;
var south = 50.7586199274002183;
var east = 8.7589530542385923;
var north = 50.7672082855122184;

var rectangle = Cesium.Rectangle.fromDegrees(west, south, east, north);
Cesium.Camera.DEFAULT_VIEW_FACTOR = 0.0001;
Cesium.Camera.DEFAULT_VIEW_RECTANGLE = rectangle;

const viewer = new Cesium.Viewer("cesiumContainer", {
    baseLayerPicker: false, animation: false, timeline: false
});


const layer = viewer.imageryLayers.addImageryProvider(
  new Cesium.IonImageryProvider({ assetId: 1085315 })
);
  </script>

 
