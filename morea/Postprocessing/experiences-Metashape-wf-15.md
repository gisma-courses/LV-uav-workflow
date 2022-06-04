---
title: "Case Study Gisselberger Spannweite"
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-15
morea_summary: 'The goal of the case study is to use the workflow documented in this module to capture sufficiently accurate and reproducible aerial images with low-cost mini-drones (< 250 grams weight).'
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - casestudy

---
# Case Study *Gisselberger Spannweite*

A case study is conducted using the [Gisselberger Spannweite](https://www.marburg.de/portal/seiten/renaturierungsmassnahme-gisselberger-spannweite-900002083-23001.html) as an example. 
The goal of the case study is to use the workflow documented in this module to capture sufficiently accurate and reproducible aerial images with low-cost mini-drones (< 250 grams weight). These images will then be used as baseline data for monitoring river restoration according to the proposed standardized processing procedure.

## Hardware
For this purpose, the DJI Mini 2 is suitable due to the cost, camera quality and the technology of collision-free straight and descent flight. Regardless of the admittedly enormous user-friendliness of the DJI HArdware, image capture would be possible with any (mini) drone. However, it should be noted that drones over 250 grams takeoff weight have significantly more constraints to consider. 

## Workflow
The planning was created using` QGroundcontrol` while respecting the protection zones as derived from `Airmap` and converted to `Litchi Mission Hub` using the `R` package `uavRmp`. Due to the challenging wind conditions, two intermediate landings for battery replacement were necessary. On-site acquisition, including set-up and tear-down, took roughly 1 hour. 

The flight was performed with a DJI Mavic Mini 2. Flight altitude longitudinal flight 70 meters AGL, flight altitude cross flight 50 meters AGL. In Metashape, the default workwlow was selected from `Workflow+->Best Practice->Ortho-no-GPS`. 


## Results 

The resolution of the Orthoimage calculated by the software is about 1.4 cm ground resolution. You will get an impression of quality if you compare the images below. On the left you can see the original image quality with 1.5 cm, on the right the quality resampled to 5 cm. 
{% include small-img-two.html url1="trees_1_5cm.png" url2="trees_5cm.png" %}  


 <br> <br>



Below in the interactive Cesium map the complete 5 cm dataset is available. Please compare the section of the *three trees*. The cesium server also resampled the image data and hence changes the quality again. 


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

 
