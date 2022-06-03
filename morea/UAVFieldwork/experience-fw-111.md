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
 - mandatory
---
# Field Guide

## Planning your Survey

It is most important that you setup your survey with an appropriate overlap for reliable stitching results. If the overlap is too small or vice versa you fly too fast you will get poor or no results. Same is with the flight altitude and the camera settings. Below you find suggested values.

| ASL Alt m | GP8MP3+ | GP12MP3+ | DJI P3 4K | MAPIR 2 |
|:---------:|:-------:|:--------:|:---------:|:-------:|
|15|1.08|0.9|0.63|0.56|
|30|2.16|1.8|1.27|1.03|
|75|5.4|4.5|3.2|2.53|
|100|7.2|6.0|4.25|3.38|

Ground Resolution of typical cameras in cm

## Suggested Overlap

Front Overlap 80%,  Side Overlap 60%

## Camera Speed

Depending on the product and manufactor of the cameras you have to deal with different speeds. NOTE: Only the speed that can be continously achieved is taken into account. Currently a picture rate of 2 sconds is the maximum in speed.

{% include note.html content=" It is strongly recommended that you use (if available) an autonoumous camera timer (time lapse) for controlling the pictures interval."
%}

## Flight Speed

On average the fasted SD Cards will be able to achieve an average speed of about 2 seconds/JPEG (Raw + JPEG 3.5 seconds) image. As a result taking pictures every 2 seconds will be a sporty attempt. The Flight speed recommodations are meeting this needs. Let us assume you fly a task with the field of view (FOV) of the DJI 4K camera at 35 meters above ground level (AGL). To derive the maximum flight distance from picture to picture in meter for the given overlap you have to calculate:

$$FOV*agl*(1-overlap) = 1,71*35*0,2 = 12 m$$ 

If you can take a picture every 2 seconds your max speed is: 

$$12 m / 2 s  = 6 m/s$$

## Rule of thumb

For  JPG pictures: $$0,15 * agl (RAW; 0,07 * agl)$$
For a 100 meter AGL flight you should set the speed to a maximum of:
 $$0,15 * 100 = 15 m/s (54 km/h)$$ 
For a flight of 35m agl this is will be roughly 5,25 m/s

## DEM/DSM Data
If you fly in an wide open flat area you do not need additional data. But if you fly in middle range mountains, forests or similar complex structures you will need a digtal surface model (DSM/DEM) for retrieving an optimal and safe flight path. 

## Weather
Actually you also should check the weather.
{% include attention.html content=" 
Forget about flying with wind speed above 4 Beaufort - the UAV is **not** a falcon."
%}

## Workflow in the field 
{% include note.html content=" 
1. Plan your flight with an adequate planning tool at home and double check control it in the field (see examples, check your flightplan)<br>
2. Setup your Remote Controller <br>
3. Setup your controlling device <br>
4. Setup your UAV <br>
5. Setup your safety system (use a parachute!) <br>
6. Setup your camera(s)<br>
7. Start RC <br>
8. Start UAV <br>
9. Start Camera <br>
10. Load Task <br>
11. Fly Task <br>
"
%}

## Pretask Check

As simple this seems it is full of pitfalls. Therefore we would like to provide some checklist:


{% include ass.html content=" 
* UAV <br>
    + batteries fully charged <br>
    + remote control charged <br>
    + props <br>
    + cables<br>
    + parachute<br>
    + cleanup MicroSD cards<br>
    + charge camera(s) <br>
    + configure camera(s)<br>
    + charger<br>
    + minute book<br>
    + power bank<br>
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

# Comments & Discussions 
{% include utter.html  %} 