---
title: "Georeferencing of imagery without GPS data"
published: true
morea_id: experience-fw-21
morea_summary: "Aligning UAV picture with no or defect GPS image positions"
morea_url: 
morea_type: experience
morea_sort_order: 21
morea_labels:
 - advanced
 - supplement
 - optional 
---

## Georeferencing of Imagery without GPS Data

This document provides a basic workflow for georeferencing Solo/Pixhawk flight data, as well as an optimized process for deriving high-quality point clouds, 3D models, and orthoimages. In detail, it covers the following topics:

- data acquisition constraints  
- geotagging of the images  
- high-quality image alignment  
- high-quality point cloud generation  
- high-quality orthoimage generation  
- high-quality dense point cloud generation  
- importing and exporting data from Metashape  
- Agisoft Metashape scripting  
- interaction with the uavRst package  

{% include note.html content="This is a preliminary draft. Please note that significant changes can still be expected." %}


## Constraints of Data Acquisition

The foundation for good micro-remote sensing products is the image quality produced by the drone. These images go through a post-processing workflow in which the initial image quality affects all further steps. The workflow is straightforward and effective if some basic constraints are kept in mind during data acquisition.

There are two main requirements:

* Sufficient overlap: Ensure that at least 70% of each photo is in focus, while avoiding scale jumps (use surface-following flight paths). Consider the footprint on which overlap is calculated — if you have structural layers at different distances to the camera, each will have its own footprint, affecting overlap.
* Diffuse but bright lighting: Ideal conditions are around noon with high, thin cirrus clouds to scatter the light evenly and reduce shadows.

## Prerequisites

This workflow requires several tools. First, you’ll need [mapillary_tools](https://github.com/mapillary/mapillary_tools), a useful set of Python scripts for positioning images on web maps. You will also need to install the following Python packages: `gpxpy`, `pillow`, `exifread`, and `pyexiv2`.  
If you’re using Windows, first install a [pip installer](https://sites.google.com/site/pydatalog/python/pip-for-windows).  
On Linux, you can install pip with:

```bash
sudo apt-get install pip
