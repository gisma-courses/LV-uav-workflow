---
title: "Aerial Tasks - Planning a Survey"
published: true
morea_id: experience-fw-13
morea_summary: "Planning an aerial flight mission using QGroundcontrol for usage with Pixhawk and DJI"
morea_url: 
morea_type: experience
morea_sort_order: 13
morea_labels:
 - basic
 - mandatory
---


<br> 

{% include cool.html content=" 

The planning of autonomous surface flights can be done free of charge, comfortably and safely with very many different software packages. The proposed workflow with QgroundControl allows the use of Pixhawk and via Litchi also DJI hardware. At the same time it offers an integration of the no-fly zones and the SRTM terrain model and thus provides the basic documentation for an aerial flight. 

"%}
<br> 


## Task

This recipe deals with the effective and safe planning of an autonomous flight. The survey flight is over high relief energy terrain to generate orthophotos and point clouds. 

[QGroundcontrol](http://ardupilot.org/planner2/) 

## General Workflow 
  1. Identify the area, digitize a polygon
  2. Adjust the flight and camera parameters to your needs 
  3. Convert and upload the mission control files either directly to your tablet/smartphone or alternatively via the Litchi cloud.
  4. Make an extensive preflight check

  
### Digitizing the survey area

### Missionplanner or Qgroundcontrol survey feature
We want to plan a flight in a structured terrain in the upper Lahn-valley. Start the `QGroundcontrol` and navigate to Mission tab and open `Pattern->Survey`. Start digitizing a pattern as you want and also fill in the values on the right sided menus for camera angel overlap and so on.

{% include medium-img.html url="qcmission.png" %}  

Save this fightplan to an appropriate folder. 

You will find a complete step by step tutorial at [Survey (Plan Pattern)](https://docs.qgroundcontrol.com/master/en/PlanView/pattern_survey.html).

## Export the plan

If finished klick on the File Button on the left side menu and save this plan choosing the KML file format. You will need this file for the next step. 

