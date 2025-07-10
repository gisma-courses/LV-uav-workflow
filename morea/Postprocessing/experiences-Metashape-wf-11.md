---
title: "Metashape Ortho+ - optimized processing of RGB images"
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-11
morea_summary: "Metashape Ortho+ extension provides a set of tools for easy reproducibility of optimized generation of orthoimages and point clouds. It is a convenient extension of the standard tools and workflows."
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - advanced
 - mandatory 

---

# Metashape Workflow via `Ortho+`

The `Metashape Ortho+` menu provides essential scripts that simplify and optimize the manual metashape workflow [Ludwig et al., 2020](https://www.mdpi.com/2072-4292/12/22/3831). The optimized workflow generates reproducible and automatically optimized products from the aerial images. Installation is seamless via Metashape's scripting interface.  
After the installation and the necessary restart of Metashape there is `Ortho+` menu item in the Metashape menu bar. 

{% include kim.html content="
The MetashapeToolbox plugin is capable to control all working steps for low cost aerial images with GPS information. Usually it is capable to replace the manual workflow.
<br>
**This is not the case for multispectral sensors like the `MicaSense Altum` or other advanced sensors!**
<br>

 " %}

### Instalation of the toolbox
**Linux/Mac:**
Download this repo and unzip it to `~/.local/share/Agisoft/Metashape Pro/scripts/`

```bash
cd ~/.local/share/Agisoft/Metashape Pro/scripts
git clone https://github.com/gisma/MetashapeTools.git .
```
**Windows:**
Copy the content of this repo to `User/AppData/Local/AgiSoft/Metashape Pro/scripts`

## First things first - Load images 
All functions are based on image data so first do **always** the following:

1. Add the images you want to process to the chunk.
2. Give the chunk a meaningful name.
3. Save the project using a meaningful name

Note: You will be always ask if you want to perfrm the task for a singel chunk or all chunks. Choose wisely.

## `BestPractice`

The `BestPractice` menu provides robust and well tested workflows that are primarily intended for processing large image data sets from (low cost) drone surveys. The problem that arises here is the huge amount of images with numerous starts and landings and a fixed continuous camera system (e.g. GoPro Hero 7, time lapse 2 sec). This way, 10k images are quickly collected, 80% of which are over sampled or of poor image quality and so on. The workflows identify low image quality and reduce the number of images by an inverse camera position calculation based on the preliminary surface model. This *dramatically* reduces the number of images, due to elimination of unusable taxiway and takeoff/landing image sequences. In addition the remaining cameras are activated and optimized. In this way, the quality and reproducibility can be significantly improved. At the same time, processing time is reduced by one to two orders of magnitude. 

## Orthoimage Workflow integrating Ground Control Points (GCPs)

It is obligatory that you run consecutively  all three steps.

### `Step-1 Orthoimage-pre-GCP`
* Start the script `Orthoimage-pre-GCP`
  * checks image Quality and drop images with  a quality less than 0.78
  * calculate a first alignment and mesh using the following parameters: 
  * key point limit: 10000
  * tie point limit: 1000
  * downsampling: 4
  * smoothing 10 times
  * reduce overlap with a value of 8 
  * calculate a **second** alignment and mesh using the following parameters: 
  * key point limit: 40000
  * tie point limit: 4000
  * downsampling: 1


### `Step-2 Link GCP to images` 


{% include kim.html content="
This is a manual step please follow the bekow instructions
 " %}
After the script is finished you *may* need to manually remove the few remaining start and landing area pictures. Otherwise you will find at the launching place some artefacts. To do so just right-click on the position in the model and choose filter by point. Mark and remove all pictures with the launching pad and repeated launching and landing images.

The procedure is well documented. Dor instant watch this [YouTube](https://youtu.be/G09r5PXqhBc) or follow this [tutorial](https://agisoft.freshdesk.com/support/solutions/articles/31000153696-aerial-data-processing-with-gcps-orthomosaic-dem-generation). Import your Ground Control Points (GCP) and align them manually in at least 4 images. Use about 30 % of the GCP as independent checkpoints by unticking the check box in the reference pane. Save your project.

### `Step-3 Optimize Sparsecloud`
Performs an iterative optimisation of the sparse cloud to retrieve the best reprojection error. The tie pointcloud will be much more reliable for all later tasks


### `Step-4 Orthoimage-post-GCP`

* Use `Orthoimage-post-GCP`. This includes the following steps:
  * optimize sparse cloud using the point cloud statistics
  * create 2.5D Mesh
  * smooth Mesh with factor 35 (empirical value for forests)
  * create Orthomosaic
	  * surface: mesh
	  * refine seamlines = True
  * export Orthomosaic, Seamlines and Marker error
  * export report

Finally you have a result that automatically tries to optimize the number of necessary cameras, minimize re projection errors in the tie point cloud (sparse cloud), re-arrange the cameras and thus produce an reproducible orthoimage on the (statistically) best possible spatial resolution. 

### `Orthoimage-no-GCP`
If you do *NOT* have Ground Control Points or not intending to squeeze the absolute position of the final product, you can run corresponding to the upper workflow, an one click production of optimized orthoimages. This maybe very useful if you have several repeated flights over an area and if you want to get an overview. Just put the image data of each flight in a seperate chunk and start the script `Toolchain noGCP` with the option to process all chunks.

This will do the following steps:.
* Check image Quality and drop images with  a quality less than 0.75
* Calculate a first alignement and mesh with 
  * Key Point Limit: 10000
  * Tie Point Limit: 1000
  * Downsampling: 4
  * Smoothing 10 times
* reduce overlap with a value of 15 
* on the remaining cameras calculate second alignment and 2.5D mesh with: 
  * Key Point Limit: 40000
  * Tie Point Limit: 4000
  * Downsampling: 1
* smooth Mesh with factor 35
* create Orthomosaic
	* surface: mesh
	* refine seamlines = True
* export Orthomosaic, Seamlines and Marker error
* export a report
## `Tools+`

### `Reduce Overlap`

Performs a low-quality initial alignment to generate a sparse point cloud and a smoothed mesh (smoothing factor: 10). Based on this, it calculates an inverse optimization of the necessary camera positions using a reduction factor of 8.

### `Densecloud`

Generates a dense point cloud based on the existing sparse cloud and alignment.

### `Orthoimage`

Use `Orthoimage` if you do **not** intend to optimize camera positions or the sparse point cloud beforehand. This script executes the following steps:

* Generate a 2.5D mesh  
* Smooth the mesh (smoothing factor: 35)  
* Create an orthomosaic:  
  * Surface: mesh  
  * Refine seamlines: `True`  
* Export:
  * Orthomosaic  
  * Seamlines  
  * Marker error report  
  * Project report  

{% include kim.html content="
It is strongly recommended to run the `Optimize Sparsecloud` script beforehand. This helps to minimize the reprojection error and improves the overall accuracy of your final orthomosaic.
" %}
  
---

## `Utilities`

### `Export Marker Error`

Exports the marker error statistics as a `.csv` file.

### `Export Tiepoint Error`

Exports key statistics from the sparse point cloud (e.g., Reconstruction Uncertainty, Reprojection Error, Projection Accuracy, Image Count) to a `.csv` file.

### `Orthomosaic Reproducibility`

1. Import your Ground Control Points (GCPs) and align them.  
2. Run the script `Reproducibility`.

This script generates a set of orthomosaics (default: 5), which can then be evaluated statistically in **R** or other analysis tools to assess spatial variability and product consistency.

---

## Further Readings

The above-described workflow functions to a certain extent as a "black box." However, it is fully documented, and you are encouraged to inspect the scripts directly and review the corresponding publication by [Ludwig et al. 2020](https://doi.org/10.3390/rs12223831).

The optimizations and workflows presented in this course are tailored primarily to low- and mid-altitude forest environments in mountainous regions. Accordingly, the presets may require adjustment for other application contexts.

That said, it is highly recommended to engage actively with the capabilities of Metashape. The resources below offer insights into diverse workflows and application scenarios. They also explain interactive tool use beyond what is scripted in `Ortho+`.

{% include note.html content="
You will likely encounter other, sometimes conflicting, recommendations in literature and practice. Feel free to experiment and share your insights with the community!
" %}

* [Aerial data processing – Orthomosaic & DEM generation](https://agisoft.freshdesk.com/support/solutions/articles/31000153696-aerial-data-processing-with-gcps-orthomosaic-dem-generation)  
* [USGS – Processing Coastal Imagery with Agisoft](https://pubs.usgs.gov/of/2021/1039/ofr20211039.pdf)  
* [Metashape 1.8 User Manual (PDF)](https://www.agisoft.com/pdf/metashape-pro_1_8_en.pdf)
