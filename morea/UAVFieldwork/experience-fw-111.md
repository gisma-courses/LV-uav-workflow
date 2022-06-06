---
title: "Field Guide"
published: true
morea_id: experience-fw-111
morea_summary: "Schemes for well-being during the field work"
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - advanced
 - recommended
---

# Field Guide

## Planning your Survey

It is most important that you setup your survey with an appropriate overlap for reliable stitching results. If the overlap is too small or vice versa you fly too fast you will get poor or no results. Same is with the flight altitude and the camera settings. Below you find suggested values.

|AGL|GP8MP3+|GP12MP3+|DJIP3-4K |MAPIR-2|DJI-Mini-2|
|:--  |:--:  |:--:  |:--:  |:--:  |:--:  |
|**15m**|1.08|0.9|0.63|0.56|0.8|
|**30m**|2.16|1.8|1.27|1.03|1.6|
|**75m**|5.4|4.5|3.2|2.53|3.9|
|**100m**|7.2|6.0|4.25|3.38|5.2|

*Ground Resolution of typical cameras in cm with respect to the above surface level.*

#### Suggested Overlap

Front Overlap 80%,  Side Overlap 60%

#### Camera Speed

Depending on the product and manufactor of the cameras you have to deal with different speeds. NOTE: Only the speed that can be continously achieved is taken into account. Currently a picture rate of 2 sconds is the maximum in speed.

{% include note.html content=" It is strongly recommended that you use (if available) an autonoumous camera timer (time lapse) for controlling the pictures interval."
%}

#### Flight Speed

On average both SD Cards and cameras will be able to achieve an average speed of about 2 seconds/image. As a result taking pictures at least every 2 seconds is a bit challenging. The Flight speed recommendations are meeting this needs. Let us assume you fly a task with the field of view (FOV) of the DJI 4K camera at 40 meters above ground level (AGL). To derive the maximum flight distance from picture to picture in meter for the given overlap you can calculate approximately:

$$FOV*agl*(1-overlap) = 1.71*35*0.2 = 12 m$$ 

If you can take a picture every 2 seconds your max speed is: 

$$12 m / 2 s  = 6 m/s = 10.8 km/h$$

##### Rule of thumb

For a 100 meter AGL flight you should set the speed to a maximum of:

$$0.2 * 100 = 20 m/s = 72 km/h$$ 

For a flight of 40m AGL this is will be roughly: $$5,25 m/s = 28.8 km/h$$

#### DEM/DSM Data
If you fly in an wide open flat area you do not need additional data. But if you fly in middle range mountains, forests or similar complex structures you will need a digtal surface model (DSM/DEM) for retrieving an optimal and safe flight path. 

## Weather
{% include attention.html content=" 
[Check the weather](https://www.windy.com/?50.117,8.684,5). 
<br>You **must** take care of the wind gusts and cloud coverage for quality and safety reasons.

<br><br>
Do **not** ignore this. **Forget** about flying with wind speed above 4 Beaufort - most UAVs are **not** falcons."
%}
<br><br>
# Workflow in the field 
<br>
{% include note.html content=" 

1. Setup your remote controler, controlling device, UAV <br>
2. Load task <br>
3. Double check if the task is correct
4. Start task <br>
5. Check always the complete situation - pilot the UAV, co-pilot the sourrounding
"
%}
<br>
## Pre-flight Check

As simple this seems it is full of pitfalls. Therefore we would like to provide some checklist:


{% include ass.html content=" 
* UAV <br>
    + batteries fully charged <br>
    + remote control charged <br>
    + props <br>
    + cleanup MicroSD cards<br>
    + field charger<br>
    + minute book<br>
    + power bank<br>
    (+ charge camera(s)) <br>
    (+ configure camera(s))<br>    
<br><br>
* Tools<br>
    + Tools for the UAV<br>
    + Tape, glue etc.<br>
    + Table, chairs etc.<br>
<br><br>
* Survey<br>
    + Survey is checked<br>
    + Task is stored on controller (app)<br>
    + offline maps loaded<br>
<br><br>
* Legal stuff<br>
    + insurance valid<br>
    + common flight permission<br>
    + specific permissions<br>
    + necessary to inform flight security authorithy<br>
    + necessary to inform local air control<br>
<br>"
%}

