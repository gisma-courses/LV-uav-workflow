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


# UAV Mission Planning - Practical Workflow

The _**open**_ UAV community is focused on the PixHawk autopilot unit and the [MissionPlanner](http://qgroundcontrol.com/downloads/), or more recent and platform independent, the [QGroundcontrol](http://ardupilot.org/planner2/) software. Both are well documented and provide APIs and easy to use GUIs. Nevertheless they are missing some planning capabilities like a high resolution terrain following flight planning or dealing with battery-dependent task splitting and save departures and approaches within the splitted main tasksor exporting the tasks to DJI compatible format yet. Other commercial competitors like the extremly powerful [ugcs](https://www.ugcs.com/) are cost intensive and/or fairly complex applications which are not handy as a lightweight planning facility. 

The `R` package [`uavRmp`](https://github.com/gisma/uavRmp) tries to bridge this gap. It generates `MAVLINK` format compliant mission files that can be uploaded to the Pixhawk controller via any Ground Control Station software. In addition it exports or converts plannings to the `Litchi` format which can be used for DJI drones.

## Installation 
´
First of all you need to install the scripting language `R` an preferably the Integrated Development Enironment (IDE) `Rstudio`. You will find a step by step tutorial at  [HowTo install R & RStudio](https://geomoer.github.io/moer-base-r/unit01/unit01-02_Installation.html). Alternatively you may use the [rig - R installation manager](https://github.com/r-lib/rig#the-r-installation-manager). Then follow the instructions at the  [`uavRmp`](https://github.com/gisma/uavRmp) homepage and install the package. Check for the most recent version. However you can install the latest stable version from `CRAN`.

``` R
install.packages("uavRmp")

```


To install the cutting edge (if so) version you should take it from `github`.  You need to have installed the `devtools` package.

``` R
install.packages("devtools")
devtools::install_github("gisma/uavRmp", ref = "master")

```

# Basic mission planning workflow

This tutorial deals with the effective and safe planning of an autonomous flight. This provides basic information about the used hardware and software as well as supplemental data and nice to haves. The basic workflow of planning a good aerial and target oriented flight mission. In the extended version you find some more explanations and hints for improving your planning. 


## Things you need 



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
We want to plan a flight in a structured terrain in the upper Lahn-valley. Start the `QGroundcontrol` and navigate to Mission tab and open `Pattern->Survey`. Start digitizing a pattern as you want and also fill in the values on the right sided menus for camera angle overlap and so on.

{% include medium-img.html url="qcmission.png" %}  

Save this fightplan to an appropriate folder. 

### Calling `makeAP` from the `uavRmd` package

There are a lot of optional arguments available that helps to control the generation of an autonomous flight plan. In this first use case we keep it as simple as possible. First we will focus the arguments to organize the project.  All results will be stored in a fixed folder structure. The root folder is set by the argument `projectDir`. e.g. `~/proj/uav`. The current working directory will then be generated from the `locationName` and is always a subfolder of the `projectDir`. So in this case it is set to `firstSurvey`.  The resulting folder for a specified location in a speciefied project is then `~/proj/uav/firstsurvey`. According to the date of planning the following subfolder structure is set up. The log files are saved in the `log` folder the temporary data sets are stored in a folder called `run`.

{% include note.html content=" 
The mission control file(s) are stored in a folder named `control`.
"%}

Please check the folder structure according to the figure below.

{% include medium-img.html url="folderstructure.png" %}  
  

#### Explanation of the used arguments

* *useMP = TRUE*   is the switch to activate and QGroundCOntrol or Missionplanner task file
* *demFn = filname* set path and filename to the used DEM 
* *surveyArea = fa* set path and filename of the QGroundControl flightplan
* *maxFlightTime = 25* set the maximum estimated lifetime of the battery in minutes
* *maxwaypoints = 250* set the number of allowed waypoints in one control file (older DJIs /Litchi were constrained by 99 waypoints)

```r
library(uavRmp)
# get example DEM data
 demFn <- system.file("extdata", "mrbiko.tif", package = "uavRmp")
 fa <- system.file("extdata", "qgc_survey.plan", package = "uavRmp")


fp = makeAP(projectDir = "~/uav",
        surveyArea=fa,
        useMP = TRUE,
        demFn = demFn,
        maxFlightTime = 25,
        maxwaypoints = 250,
        uavType = "dji_csv")                 
```

The script generates:

  * R objects for visualisation
  * log file(s) 
  * flight control file(s) for running a mission on DJIs 

All  of them are important even if a quick inspection of the generated objects is the maxFlightTime which rules the length of the single flight. The log file dumps  all important parameters of the calculated mission.

If you just want to convert fight plans from `GroundControl` to `Litchi` You may also use the shiny GUI:
```r
library(uavRMp)
library(shiny)
runApp(system.file("shiny/plan2litchi/", "/app.R", package = "uavRmp"))
```

Just navigate as requested to the files and check the output. Be patient it may take a while.
{% include medium-img.html url="shiny.png" %}  

After checking the files you should import the control file to the [Litchi Hub](https://flylitchi.com/hub). You need an account. During the course the account and Litchi Software is provided via Ilias. 

 <br> <br>
{% include cool.html content="
Ready to take off - that’s your first flight plan!"
%}

 <br> <br>
