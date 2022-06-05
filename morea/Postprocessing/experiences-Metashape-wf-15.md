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

## Planning



The planning was created using` QGroundcontrol` while respecting the protection zones as derived from `Airmap` and converted to `Litchi Mission Hub` using the `R` package `uavRmp`.

The flight was performed with a DJI Mavic Mini 2. Flight altitude longitudinal flight 70 meters AGL, flight altitude cross flight 50 meters AGL. Camera lapse rate was set to 2 seconds
<iframe src="https://flylitchi.com/hub?m=GoaB3rae3J" height="600px" width="100%" frameborder="0" onload="resizeIframe(this)" ></iframe>
<iframe src="https://flylitchi.com/hub?m=cg0TRo2KdE" height="600px" width="100%" frameborder="0" onload="resizeIframe(this)" ></iframe>

Due to the challenging wind conditions and with respect to flight saftey, two intermediate landings for battery replacement were necessary. On-site acquisition, including set-up and tear-down, took roughly 1 hour. 

## Post-Processing

Data Processing was carried out using `Metashape's` addon `Workflow+->Best Practice->Ortho-no-GPS`. TheGround Pixel Sample size was set to 1.5 cm. 


## Results 

### Resolution issues
The resolution of the Orthoimage calculated by the software is about 1.4 cm ground resolution. You will get an impression of quality if you compare the images below. 
{% include small-img-two.html url1="trees_1_5cm.png" url2="trees_5cm.png" %}  

*On the left you can see the original image quality with 1.5 cm, on the right the quality resampled to 5 cm.*

 <br>
### Overall visual inspection
Below in the upper Cesium map you will find an interactive map of the complete 5 cm orthoimage. Please compare the section of the *three trees* with the Cesium rendering. You will note that the cesium server also resample the image and hence changes the visual quality again. Inaddition you can check how the quality of the automatic genberated reolocation applies to the web based maps. Check the **?** Button for navigation help.
 <br>
<iframe src="cesium_ortho_1.html" height="800px" width="100%" frameborder="0" onload="resizeIframe(this)" ></iframe>

 <br>
### Mesh with texture
In the lower panel you will find the textured meshgrid.  Please notice this the unsmoothed raw mesh. It has to be located manually so the 3D placement may be a bit arbitrary.
 <br>
<iframe src="cesium_ortho_2.html" height="850px" width="100%" style="border:none;"></iframe>