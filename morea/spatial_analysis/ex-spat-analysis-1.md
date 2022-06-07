---
title: "OBIA Workflow QGIS"
toc: true
toc_label: Inhalt
published: true
morea_id: ex-spat-analysis-1
morea_summary: "The basic Object-based image analysis (OBIA) workflow with QGIS and the OTB processing plugin follows a straightforward approach. This Tutorial shows the most common way."
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - basic
 - mandatory 
 - YouTube ~18min
 - preliminary

---

# Object-based image analysis (OBIA) with QGIS and OTB processing plugin



## The complete OBIA Workflow 
{% include youtube.html id="fX2UpOwoYLk" %}

## Step by step

### Segmentation

In the search field of the `Processing Toolbox`, type *segmentation* and double click `Segmentation`.

* select the input image: `lahn-gi-spann.tif`
* select `meanshift` from the drop-down list `Segmentation algorithm`
* The `Range radius` value can be set to **25**. We are dealing with RGB images that have a range `0-255`. The optimal value depends on datatype dynamic range of the input image and requires experimental trials for the specific classification objectives.
* Set `Minimum Region size` in pixels to **16**. This is determing the spatial range of the segementation and is also experimental. Try to identify the scale of your major classes in pixel.
* keep `Processing mode`  as `Vector`
* Set `Mask image` to `empty` the blank entry of the drop-down list
* Tick `8-neighborhood connectivity` on.
* Set `Minimum object size` in pixels to `16` depending on the minimum mapping size and according to your targeted object size.
* Name the `Output vector file`  as  `lahn-gi-spann-segments-meanshift.shp`. You must write the extension `.shp` in this module.
* Push `Run`.

[[screenshot1]]

Evaluate the segmentation results: 
* Load the output vector file `lahn-gi-spann-segments-meanshift.shp` into your QGIS session and place it on top of the image `lahn-gi-spann.tif`
* Colorize the vector layer in the QGIS Layers window. Right click `Properties->Symbology->Simple Fill`, `Fill Style`: `No Brush` and `Stroke color`: `white`.

### Feature extraction 
Type `zonalstats` in the search field of the Processing Toolbox and open `ZonalStatistics` which is settled under the image manipulation section of OTB.

* Select as input image: `lahn-gi-spann.tif`.
* Select `input vector data` the vector file with segments from above segmentation `lahn-gi-spann-segments-meanshift.shp`
* Name for the `output vector`: `lahn-gi-spann-segments-meanshift-zonal.gpkg`.
* Push `Run`.

[[screenshot2]]

### Training
Type `train` in the search field of the Processing Toolbox and open `TrainVectorClassifier`

* In the  field  `Vector Data List` select *manually** a vector file clicking **...** and browse directly to the file containing the training area polygons `lahn-gi-spann-segments-stats.gpkg`.
* Provide the `Output model filename` as `lahn-gi-spann-obia.model`
* In the field `Field names for training features` copy and paste <pre> "mean_2 stdev_0 mean_9 mean_7 mean_0" </pre>
* The name of `Field containing the class id for supervision` is `CLASS_ID`.
* Classifier to use for training: `libsvm`
* SVM Kernel Type: `linear`
* SVM Model Type: `csvc`
* tick `Parameters optimization` to `ON`.
* Push `Run`

[[screenshot3]]


### Classification phase
Type `class` in the search field of the Processing Toolbox and open `VectorClassifier`
*  In the  field  `Vector Data` select *manually** a vector file clicking **...** and browse directly to the file containing the training area polygons containing segments and features for the whole image `lahn-gi-spann-segments-meanshift-zonal.gpkg`.
* The name of the upper `input model` file is `lahn-gi-spann-obia.model`
* Output field containing the class is `CLASS_ID`
* Copy and paste into the field `Field names to be calculated` same attributes as above <pre> "mean_2 stdev_0 mean_9 mean_7 mean_0" </pre>
* Name the `output vector` data `lahn-gi-spann-classified_obia.gpkg`.
* Push `Run`.

[[screenshot4]]

Load the output vector file into QGIS and apply the same QGIS style used for the training data. `Layer->Layer properties->Symbology->Style->Load style...`.

