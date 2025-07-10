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

Metashape Ortho+ - optimized processing of RGB images
=====================================================

The Metashape Ortho+ menu provides essential scripts that streamline and optimize the manual Metashape workflow (Ludwig et al., 2020). It enables reproducible and automatically optimized processing of aerial imagery. Installation is seamless via Metashape's scripting interface.

Once installed and Metashape restarted, the Ortho+ menu becomes available in the Metashape menu bar.

Note: The MetashapeToolbox plugin can automate all workflow steps for low-cost aerial images with GPS metadata. In many cases, it replaces the manual workflow. This does not apply to multispectral sensors like the MicaSense Altum or other advanced sensors.

Installation of the Toolbox
---------------------------
Linux/Mac:
Download and extract the repository into:
~/.local/share/Agisoft/Metashape Pro/scripts/

cd ~/.local/share/Agisoft/Metashape Pro/scripts
git clone https://github.com/gisma/MetashapeTools.git .

Windows:
Copy the repository contents into:
User/AppData/Local/Agisoft/Metashape Pro/scripts

First Things First – Load Images
--------------------------------
All functions are based on image data. Therefore, always start with:

1. Add the images you want to process to the chunk.
2. Assign a meaningful name to the chunk.
3. Save the project with a meaningful filename.

Note: For many operations, you'll be asked whether to process a single chunk or all chunks. Choose appropriately.

BestPractice
------------
The BestPractice menu provides tested workflows tailored for large image datasets from low-cost UAV surveys. A common issue is excessive image volume due to frequent takeoffs, landings, and continuous time-lapse cameras (e.g., GoPro Hero 7, 2s interval). Often, 80% of such images are redundant or low-quality.

The BestPractice workflows:
- Detect poor-quality images
- Remove unnecessary photos (e.g., takeoff/landing)
- Optimize the camera set using inverse geometry and surface model analysis

The result is a significant reduction in image count, improved reproducibility, and processing time cut by one or two orders of magnitude.

Orthoimage Workflow with Ground Control Points (GCPs)
-----------------------------------------------------
This workflow includes four consecutive steps. All must be completed in order.

Step-1 Orthoimage-pre-GCP
--------------------------
Run Orthoimage-pre-GCP, which:
- Filters out images with quality < 0.78
- Performs a first alignment and mesh with:
  Key Point Limit: 10,000
  Tie Point Limit: 1,000
  Downsampling: 4
  Smoothing: 10x
  Overlap reduction: 8
- Performs a second alignment and mesh with:
  Key Point Limit: 40,000
  Tie Point Limit: 4,000
  Downsampling: 1

Step-2 Link GCP to Images
-------------------------
After the script completes, you may need to manually remove remaining takeoff/landing photos.
Right-click the area in the model, choose "Filter by Point", then select and delete unwanted images.

Follow this YouTube video or Agisoft tutorial:
- https://youtu.be/G09r5PXqhBc
- https://agisoft.freshdesk.com/support/solutions/articles/31000153696-aerial-data-processing-with-gcps-orthomosaic-dem-generation

Import your GCPs and align each to at least 4 images. Use about 30% of GCPs as independent checkpoints by unticking them in the Reference pane. Save your project.

Step-3 Optimize Sparse Cloud
----------------------------
This step performs iterative optimization of the sparse point cloud to minimize reprojection error and enhance point reliability.

Step-4 Orthoimage-post-GCP
---------------------------
Run Orthoimage-post-GCP. It:
- Optimizes the sparse cloud using point statistics
- Creates a 2.5D mesh
- Smooths the mesh (factor: 35)
- Creates orthomosaic with:
  Surface: mesh
  Refine seamlines: true
- Exports:
  Orthomosaic
  Seamlines
  Marker error report
  Project report

This generates a reproducible orthoimage based on statistically optimized camera positions.

Orthoimage-no-GCP
-----------------
If no GCPs are available or needed, you can produce an optimized orthomosaic with one click:

- Place each flight’s image data in a separate chunk
- Run Toolchain noGCP and process all chunks

The script:
- Filters images with quality < 0.75
- First alignment and mesh:
  Key Point Limit: 10,000
  Tie Point Limit: 1,000
  Downsampling: 4
  Smoothing: 10x
- Overlap reduction: 15
- Second alignment and 2.5D mesh:
  Key Point Limit: 40,000
  Tie Point Limit: 4,000
  Downsampling: 1
- Smooths mesh (factor 35)
- Creates and exports:
  Orthomosaic (mesh surface, refine seamlines = true)
  Seamlines and marker errors
  Report

Tools+
------
Reduce Overlap
- Performs a quick alignment and mesh (smoothed with factor 10)
- Optimizes image selection with reduction factor 8

Densecloud
- Generates a dense point cloud

Orthoimage
- Creates 2.5D mesh
- Smooths mesh (factor 35)
- Generates orthomosaic (mesh surface, seamlines refined)
- Exports orthomosaic, seamlines, marker error, and report

Tip: Run "Optimize Sparsecloud" before for minimal reprojection error.

Utilities
---------
Export Marker Error
- Exports marker errors to CSV

Export Tiepoint Error
- Exports sparse cloud errors (e.g., reprojection, uncertainty) to CSV

Orthomosaic Reproducibility
- Import and align GCPs
- Run "Reproducibility" script
- Generates several orthomosaics (default: 5) for later analysis in R

Further Readings
----------------
Although this workflow simplifies processing, it’s a black box in many ways. For deeper insight, see:
- Ludwig et al. 2020: https://doi.org/10.3390/rs12223831

Note: Parameters are optimized for forested low/mid-mountain areas and may not fit all scenarios.

Additional Resources:
- https://agisoft.freshdesk.com/support/solutions/articles/31000153696-aerial-data-processing-with-gcps-orthomosaic-dem-generation
- https://pubs.usgs.gov/of/2021/1039/ofr20211039.pdf
- https://www.agisoft.com/pdf/metashape-pro_1_8_en.pdf

Remember: you will encounter different, even contradictory, recommendations elsewhere. Try things out — and share your experiences.
