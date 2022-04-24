---
title: "Metashape Toolbox - optimized processing of RGB images "
toc: true
toc_label: Inhalt
published: true
morea_id: experience-metashape-wf-31
morea_summary: "Agisoft Metashape basic workflow"
morea_url: 
morea_type: experience
morea_sort_order: 31
morea_labels:
 - optional
 - advanced
 - practices
 - 15 min

---

# Metashape Workflow via Metashape Toolbox

The Metashape Toolbox provides essential scripts that simplify and optimize the manual metashape workflow [Ludwig et al., 2020](https://www.mdpi.com/2072-4292/12/22/3831). The optimized workflow generates reproducible and witgehend automatically optimized products from the aerial images. Installation is seamless via Metashape's script interface.  
After the installation and the necessary restart of MEtashape there is a optimizeTools menu item in the Metashape menu bar. 

{% include kim.html content="
The MetashapeToolbox plugin is capable to control all working steps for low budget cameras like GoPro etc.. Usually it replaces the manual workflow.
<br><br>
**This is not the case for specific sensors like the MicaSense Altum or other advanced sensors!**
<br><br>
However you preferably should integrate in [specific workflows](https://agisoft.freshdesk.com/support/solutions/articles/31000148381-micasense-altum-processing-workflow-including-reflectance-calibration-in-agisoft-metashape-professi) the MetashapeToolbox functions if appropriate.
 " %}

### Instalation of the toolbox
**Linux/Mac:**
Download this repo and unzip it to `~/.local/share/Agisoft/Metashape Pro/scripts/`

```bash
cd ~/.local/share/Agisoft/Metashape Pro/scripts
git clone https://github.com/envima/MetashapeTools.git .
```
**Windows:**
Copy the content of this repo to `User/AppData/Local/AgiSoft/PhotoScan Pro/scripts`

### Procedure of toolbox usage

1. Add the images/image folders which you want to process to the chunk(s).
2. Give the chunk a meaningful name.
3. Start the script `Toolchain Part 1`. This will align all chunks and all images with the suggested and robust default parameters:
  - Key Point Limit: 40000
  - Tie Point Limit: 4000
  - Downsampling: 1

4. Import your Ground Control Points (GCP) and align them manually in at least for four images. Use about 30 % of the GCP as independent Checkpoints by unticking the checkbox in the Reference Pane.
5. Optimize the georeferencing of the product with the script `Optimize Sparsecloud`. This will print out a Reprojection Error for wich the checkpoint error is at its minimum.
6. Start `Toolchain Part 2`. This includes the following steps:
  * create 2.5D Mesh
  * smooth Mesh with factor 35
  * create Orthomosaic
	  * surface: mesh
	  * refine seamlines = True
  * export of Orthomosaic, Seamlines and Marker error


### Sensitivity study on the reproducibility of the orthophoto
1. Follow Steps 1 - 4 form above
2. Start the script `Reproducibility`
This will compute a set amount of orthomosaics (default is 5), which later can be analysed in R.


### Point cloud processing only
1. UAS Denseclouds had variying absolute height values
    - Stems from the photogrammetric process itself
    - has to be investigated at some point

2. Filtered Denseclouds by removing low confidence values
    - confidence value corresponds to the number of depth maps the point appears in
    - Low values - low amount of depth maps
    - Used a threshold of 3 to filter the denseclouds
    - [deep3d.co.uk/2020/05/10/confidence-is-everything](https://deep3d.co.uk/2020/05/10/confidence-is-everything/)

3. Normalized heights with the LiDAR based DEM
    - also for the UAS clouds
    - Terrain should not differ
    - it is reasonable to assume that there is a 1x1 m terrain model available


### Dense cloud export from Metashape

Currently there is no way in the Metashape API to conveniently export only parts of the densecloud. Here is a workaround in the Metashape interface:
1. import  shape
2. select shape
3. select point by shape
4. assign class "unclassified" to selected points
5. export points: select class "unclassified"

