---
title: "UAV Mission Planning Practical Workflow"
published: true
morea_id: experience-fw-11
morea_summary: "Planning an aerial flight mission using QGroundcontrol and uavRmp"
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - advanced
 - mandatory
---


<br> 

{% include attention.html content=" 
You will have a lot of chances to make a small mistake what may yield in a damage of your UAV or even worse in involving people, animals or non-cash assets. Check your risk - implement a **double check** system while planning and performing autonomous flight missions. Operating (autonomous) UAVs is in the full responsibility of the pilot. 
<br>
Keep cool - **keep alert!**
"%}
<br> 


# UAV Mission Planning Practical Workflow

The _**open**_ UAV community is focused on the PixHawk autopilot unit and the [MissionPlanner](http://qgroundcontrol.com/downloads/), or more recent and platform independent, the [QGroundcontrol](http://ardupilot.org/planner2/) software. Both are well documented and provide APIs and easy to use GUIs. Nevertheless they are missing planning capability (APM Planner) of a _*terrain following*_ autonomous flight planning, that is also dealing with battery-dependent task splitting and save departures and approaches yet. Other commercial competitors like the extremly powerful [ugcs](https://www.ugcs.com/) software package are fairly complex and still lacking an advanced capability for generating smooth and save surface following hull curves for low AGL altitudes.

The `uavRmd` tries to bridge this gap. It generates `MAVLINK` format compliant mission files that can be uploaded to the Pixhawk controller via any Ground Control Station software. To install from `github`  you need to have installed the `devtools` package.

``` R

devtools::install_github("gisma/uavRmp", ref = "master")

```

## Basic mission planning workflow

### Overview of the task

This recipe deals with the effective and safe planning of an autonomous flight. This provides basic information about the used hardware and software as well as supplemental data and nice to haves. The basic workflow of planning a good aerial and target oriented flight mission. In the extended version you find some more explanations and hints for improving your planning. 


## Things you need 

  - [HowTo install R & RStudio](https://geomoer.github.io/moer-base-r/unit01/unit01-02_Installation.html)
  - [uavRmp](https://github.com/gisma/uavRmp) package
  - [Digital Surface Model](https://land.copernicus.eu/imagery-in-situ/eu-dem/eu-dem-v1.1/view
) Account needed.
  - [QGroundcontrol](http://qgroundcontrol.com/)
  - Time to work it out

## General Workflow 

  1. Identify the area, digitize/type the coords of 3 corners and the launching position
  2. Adjust the flight parameters to your needs and generate flight control files
  3. Convert and upload the mission control files either directly to your tablet/smartphone or alternatively via the Litchi cloud.
  4. Make an extensive preflight check
  5. Fly the mission
  
## Basic examples 

The first example will introduce you to the basic usage and folder structure.

Purpose: Survey flight over high relief energy terrain to generate orthophotos and point clouds. 
Addressed issues:
  - Create a reliable DSM for near surface retrieval of high resolution pictures

### Digitizing the survey area

### Missionplanner or Qgroundcontrol survey feature
We want to plan a flight in a structured terrain in the upper Lahn-valley. Start the `QGroundcontrol` and navigate to Mission tab and open `Pattern->Survey`. Start digitizing a pattern as you want and also fill in the values on the right sided menus for camera angel overlap and so on.

{% include medium-img.html url="qcmission.png" %}  

Save this fightplan to an appropriate folder. 

### Calling makeAP from the uavRmd package

There are a lot of optional arguments available that helps to control the generation of an autonomous flight plan. In this first use case we keep it as simple as possible. First we will focus the arguments to organize the project.  All results will be stored in a fixed folder structure. The root folder is set by the argument `projectDir`. e.g. `~/proj/uav`. The current working directory will then be generated from the `locationName` and is always a subfolder of the `projectDir`. So in this case it is set to `firstSurvey`.  The resulting folder for a specified location in a speciefied project is then `~/proj/uav/firstsurvey`. According to the date of planning the following subfolder structure is set up. The log files are saved in the `log` folder the temporary data sets are stored in a folder called `run`.

{% include note.html content=" 
The mission control file(s) are stored in a folder named `control`.
"%}

Please check the folder structure according to the figure below.

{% include medium-img.html url="folderstructure.png" %}  
  

#### Explanation of the used arguments

* *useMP = TRUE*   is the switch to activate and QGroundCOntrol or Missionplanner task file
* *flightAltitude = 120* is set to the (legal) maximum flight altitude of of 120 meter, 
* *flightPlanMode = "track"* to activate a track flight
* *demFn = filname* the path to the used DEM 

```r

# get example DEM data
 fn <- system.file("extdata", "mrbiko.tif", package = "uavRmp")
 fa <- system.file("extdata", "qgc_survey.plan", package = "uavRmp")


fp = makeAP(projectDir = "~/uav",
        surveyArea=fa,
        useMP = TRUE,
        demFn = fn,
        maxFlightTime = 25,
        uavType = "dji_csv")                 
```

The script generates:

  * R objects for visualisation
  * log file 
  * flight control file(s). 

All three of them are important even if a quick inspection of the generated objects is most of the time sufficient. The log file dumps the all important parameters of the calculated mission. Most important the calculated mission speed and picture rate based on an estimation of the mission time. 

You may also use the shiny GUI:
```r
runApp(system.file("shiny/plan2litchi/", "/app.R", package = "uavRmp"))
```
 <br> <br>
{% include cool.html content="
Ready to take off - that’s your first flight plan!"
%}

 <br> <br>
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
