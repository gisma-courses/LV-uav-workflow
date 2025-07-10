---
title: " Metashape basic workflow "
published: true
morea_id: experience-metashape-wf-10
morea_summary: "The Metashape software provides a very slim standard workflow with reasonable default values. This tutorial gives some additional explanations for the initial exercises to create an otho image and a point cloud."
morea_url: 
morea_type: experience
morea_sort_order: 10
morea_labels:
 - basic
 - mandatory 
---

# Agisoft Metashape basic workflow

Even though Metashape is neither open source nor free, it is a powerful tool for deriving point clouds and various surface models from standard RGB imagery. It offers a user-friendly interface and strikes a good balance between hardware requirements and cost-efficiency. For more advanced use, understanding the detailed settings is essential.

## Add the photos to Metashape

Let’s begin by following the white rabbit.

After importing your aerial images into Metashape, they will appear arranged along the flight path, as shown below.

{% include medium-img.html url="workflow_image_2.png" %}

### Alignment

{% include note.html content="

The quality of the alignment is crucial for **all** downstream products — especially 3D dense point clouds and orthoimages.
"%}

The **Align Images** process is somewhat explorative. For a quick start, it’s useful to apply the following recommended settings:

{% include medium-img.html url="workflow_image_3.png" %}

This will provide a good initial assessment of how well your data can be aligned.

{% include note.html content="

We used **reference preselection** because the images are georeferenced.
"%}

However, alignment quality depends greatly on sensor type, lighting conditions, and surface characteristics. For high-quality imagery, increasing the keypoint limit beyond 240,000 generally leads to no [significant](http://www.agisoft.com/forum/index.php?topic=3559.0) improvements. As a rule of thumb, calculate the maximum number of keypoints as *megapixels × 6400*.

{% include medium-img.html url="workflow_image_4.png" %}

For images from GoPro, Mapir, or DJI cameras, this results in about 77,000 keypoints. Setting the parameters to zero tells Metashape to use the maximum, which can work well if you later filter your point clouds and models. A typical high-quality setup might look like this:

{% include note.html content="

Keep in mind that high-quality alignment will significantly increase processing time.

Also note: if your imagery is of poor quality or the alignment is unstable, using maximum settings may lead to excessive clutter and spurious tie points in the sparse cloud — which may be hard to clean up afterward.
"%}

### Creating high-quality sparse (tie) point clouds

The key to producing a clean sparse point cloud is minimizing noise and achieving accurate spatial alignment. In practice, this means obtaining the best possible image alignment and then refining it through filtering and camera optimization. If needed, you can further improve results using Ground Control Points (GCPs).

We’ve had good experience following [juhutan](http://www.agisoft.com/forum/index.php?action=profile;u=179074), who recommends this [workflow](http://www.agisoft.com/forum/index.php?topic=3559.0) for high-quality point cloud generation. Typically, only one iteration of the following steps is required:

  1. Remove sparse points via gradual selection (see below)
  2. Optimize cameras (after **each** removal)
  3. Optionally repeat steps 1–2 until reconstruction error is minimized

Explanation:
- Step 1 removes spurious points from the cloud and smooths surfaces.
- Step 2 updates all cameras to reflect the improved geometry.

#### Gradual Selection Process

Before beginning, right-click on your current chunk in the Workspace panel and choose “Duplicate Chunk” to preserve a backup.

  1. Select `Reconstruction Uncertainty`, enter a value like `10`, click OK, and press `DEL` to delete the selected points. If `DEL` doesn’t work, click inside the model window first.
  2. Then select `Reprojection Error`, set it to `< 1`, delete selected points, and click the wand icon again.
  3. Finally, choose `Projection Accuracy`, and delete the lowest `10%` of points.

More details can be found in this tutorial by [dinosaurpaleo](https://dinosaurpalaeo.wordpress.com/2015/10/11/photogrammetry-tutorial-11-how-to-handle-a-project-in-agisoft-photoscan/).

{% include note.html content="

It’s strongly recommended to follow this process if your goal is to generate high-quality point clouds, textures, or orthoimages. Though the steps are manual, the time invested will pay off.
"%}

## Build 3D model (mesh)

You can now use the refined sparse cloud to build a 3D model. The process is straightforward. For best results and a high face count in the mesh, use the following settings:

{% include medium-img.html url="workflow_image_5.png" %}

## Generate Orthophoto

Creating an orthoimage is also a straightforward process, slightly different from generating a dense point cloud. Follow this workflow:

  1. Load the prepared images
  2. Check image quality
  3. Align images as described earlier
  4. Build the mesh using the optimized sparse point cloud
  5. Generate the orthoimage based on the mesh

Using a mesh-based surface generally produces better results for low-altitude imagery. However, whether to use a dense or sparse point cloud depends on your dataset. In many cases, a well-processed sparse cloud will deliver better ortho results.

Recommended settings:

{% include medium-img.html url="workflow_image_6.png" %}

Et voilà — you now have a high-quality orthoimage.

## Creating high-quality dense point clouds

Micro-remote sensing often works with a single spectral band (RGB), but its main advantage over LiDAR is the ability to repeatedly and flexibly observe the surface over time. With Metashape, dense clouds can still be structured into layers, depending on what is visible in the data. For example, deciduous forests can be analyzed in winter (to detect terrain and tree structure) or summer (to model the canopy surface).

Dense clouds can be exported in various formats for further use in QGIS, SAGA, or 3D modeling tools. This makes it easy to integrate with established workflows originally developed for LiDAR or photogrammetry.

Note: The dense cloud settings control both quality and processing time. Higher quality means longer processing. 
- **Aggressive filtering** is fast but may lose detail.
- **Moderate or mild filtering** retains finer structures but requires more time.

You can calculate the dense point cloud after the images are aligned. Although it's listed earlier in Metashape’s workflow dropdown, it is often smarter to generate the orthoimage first, as dense cloud creation is by far the most time-consuming step.
