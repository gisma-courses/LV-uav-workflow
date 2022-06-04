---
title: "Metashape Workflow+ - optimized processing of RGB images"
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-15
morea_summary: Case Study *Gisselberger Spannweite*
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - advanced
 - mandatory 

---



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
 
