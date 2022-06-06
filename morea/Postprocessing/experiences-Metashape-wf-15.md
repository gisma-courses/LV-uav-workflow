---
title: "Use Case Gisselberger Spannweite"
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-15
morea_summary: 'The objective of this feasibility test is to evaluate the postulated workflow for its efficiency and applicability.The goal is to acquire and compute sufficiently accurate (< 2.5 cm) and reproducible orthoimages using low-cost mini-UAVs (< 250 g weight) with minimal effort.'
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - casestudy

---
# Use Case  *Gisselberger Spannweite*

A feasability study is conducted using the [Gisselberger Spannweite](https://www.marburg.de/portal/seiten/renaturierungsmassnahme-gisselberger-spannweite-900002083-23001.html) as an typical example application. 
The objective of this feasibility test is to evaluate the postulated workflow for its efficiency and applicability to acquire and compute sufficiently accurate (< 2.5 cm) and reproducible orthoimages using low-cost mini-UAVs (< 250 g weight) with minimal effort.The calculated orthoimages and point clouds are used as basic data, for example, for monitoring the development of river restoration measures.

## UAV-Hardware

UAVs that are lighter than 250 grams are especially suitable for such a purpose. The main reasons are:

 * no EU A1/A3 certificate required
 * flying in the category OPEN A1 is possible (proximity of uninvolved people and flight in cities / residential areas is possible (Attention: flight zones / no-fly zones and conditions to be observed!)
 * only identification obligation (registration of the drone owner with UAS operator ID (e-ID) and liability insurance).

For the current test, the `DJI Mavic Mini 2` was used which is a good alternative due to the connection to the proven and in use `Litchi` software and the collision-free straight and descent flight. However, with minor adjustments, the `Xiaomi Fimi X8 Mini`, which is considerably less expensive when first purchased, should also produce comparable results.  So it can be expected that such aerial imaging is possible with the better mini-Uavs. UAVs heavier than 250 grams have better cameras and flight characteristics anyway and are established for capturing such image data.  However, it should be noted that above 249 grams takeoff weight, there is a much higher planning and implementation effort to be considered due to the legal ordinances and regulations. 

## Planning

An standarized optimized planning (two flight altitudes at different angles and with 5° tilted nadir) was performed using the `QGroundcontrol`  survey with the `DJI Mini 2` camera setup and  while respecting the protection zones as derived from `Airmap` and converted to `Litchi Mission Hub` using the `R` package `uavRmp`. In addition, and take this as **obligatory**, using the  `Litchi Mission Hub` tool, during a final Point by point check, unnecessary waypoints were manually deleted or moved (you need to activate `Settings->Use Online Elevation`) to obtain an optimal flight in terms of safety, coverage and maximum of 20 minutes of battery time. You will find the two final plannings for the lengthwise flight 50 meters AGL, cross flight 70 meters AGL below. In addition the camera lapse rate was set to 2 seconds. 

The whole on-site acquisition, including set-up and tear-down, took roughly 1 hour. 
<br>
### Lengthwise flight

<iframe src="https://flylitchi.com/hub?m=cg0TRo2KdE" height="600px" width="100%" frameborder="0" onload="resizeIframe(this)" ></iframe>

<br>
### Transverse flight

<iframe src="https://flylitchi.com/hub?m=GoaB3rae3J" height="600px" width="100%" frameborder="0" onload="resizeIframe(this)" ></iframe>




## Post-Processing

In the `Metashape` workflow some tuning possibilities have not been considered yet. The following results should be interpreted against this background. 
Data Processing was carried out using `Metashape's` addon `Workflow+->Best Practice->Ortho-no-GPS`. TheGround Pixel Sample size was set to 1.5 cm. 


## Results 

For the first overview, especially the quality of the images as well as the number of artifacts and the positional accuracy are important for a visual inspection. 

### Resolution issues
The resolution of the Orthoimage is defined by a medium estimation of the two flightaltitudes. `Metashape` gives a value is about 1.4 cm ground resolution. The resulting image roughly 2.4 GB of size. If this is resamled to 5 cm we will have about 210 MB.  You will get an impression of quality loss if you compare the two cutout images below. 

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

## Conclusions 

The above example shows the efficiency of the chosen approach to collect high quality orthoimages and point clouds for nature conservation monitoring and other tasks with a low cost drone in a standardized workflow. 