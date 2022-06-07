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

### Step-1 Create Training Sample Points by manual digitizing 
You may follow this [instructions](https://geomoer.github.io/geoAI//unit02/unit02-03_digitize_training_areas.html). However we just digitize Points and not areas (polygons). 

Create a point vector file and digitize the following classes:

|class| CLASS_ID|
|:-- | --:|
|water|1|
|meadows|2|
|bare-soil-dry|3|
|bare-soil-mud|4|
|green-trees-shrubs|5|
|dead-wood|6|
|artificial-other|7|


Provide at minimum 20 sampling points.

Save this file naming it `sample.shp`.

### Step-2 Segmentation

In the search field of the `Processing Toolbox`, type *segmentation* and double click `Segmentation`.

* select the `input image`: **lahn-gi-spann-5-utm.tif**
* select `meanshift` from the drop-down list **Segmentation algorithm**
* The `Spatial Radius` value can be set to **25**.This is determining the spatial range of the segementation and is also experimental. Try to identify the scale of your major classes in pixel.
* The `Range Radius` value can be set to **25**. We are dealing with RGB images that have a range `0-255`. The optimal value depends on datatype dynamic range of the input image and requires experimental trials for the specific classification objectives.
* Set `Minimum Region size` in pixels to **25**. Minimum size of a region (in pixel unit) in segmentation. Smaller clusters will be merged to the neighboring cluster with the closest radiometry.
* keep `Processing mode`  as **Vector**
* Tick `8-neighborhood connectivity` on.
* Set `Minimum object size` in pixels to **20** 
* Name the `Output vector file`  as  **lahn-gi-spann-segments-meanshift.gpkg**. 
* Push `Run`.

{% include medium-img.html url="obia1.png" %} 

Evaluate the segmentation results: 

* Load the output vector file **lahn-gi-spann-segments-meanshift.shp** into your QGIS session and place it on top of the image **lahn-gi-spann.tif**
* Colorize the vector layer in the QGIS Layers window. Right click `Properties->Symbology->Simple Fill`, `Fill Style`: `No Brush` and `Stroke color`: `white`.

###  Step-3 Feature extraction 
Type `zonalstats` in the search field of the Processing Toolbox and open `ZonalStatistics` which is settled under the image manipulation section of OTB.

* Select as input image: **lahn-gi-spann.tif**.
* Select `input vector data` the vector file with segments from above segmentation **lahn-gi-spann-segments-meanshift.shp**
* Name for the `output vector`: **lahn-gi-spann-segments-meanshift-zonal.shp**.
* Push `Run`.

{% include small-img.html url="obia2-zonal.png" %} 

## Step-4 Joining training data with segements

In the search field of the `Processing Toolbox`, type *join* and double click `Join Attributes by Location`.

* select the `Base Layer`: **lahn-gi-spann-meanshift-zonal-stat.shp**
* select the `Join Layer`: **sample.shp**
* `Join Type`: choose **Take Attributes of the first matching...**
* Tick `Discard records which could not be joined`
* Provide an output filename
{% include small-img.html url="obia3-join.png" %} 


###  Step-5 Training
Type `train` in the search field of the Processing Toolbox and open `TrainVectorClassifier`

* In the  field  `Vector Data List` select  the correct vector file clicking **...** and browse directly to the file containing the training area polygons **lahn-gi-spann-meanshift-zonal-stat.shp**.
* Provide the `Output model filename` as **lahn-gi-spann-obia.model**
* In the field `Field names for training features` copy and paste `"mean_0 stdev_0 mean_1 stdev_1 mean_3 stdev_3"`
* The name of `Field containing the class id for supervision` is `CLASS_ID`.
* Classifier to use for training: `libsvm`
* SVM Kernel Type: `linear`
* SVM Model Type: `csvc`
* tick `Parameters optimization` to `ON`.
* Push `Run`

{% include small-img.html url="obia5-train.png" %} 


###  Step-6 Classification 
Type `class` in the search field of the Processing Toolbox and open `VectorClassifier`
*  In the  field  `Vector Data` select *manually** the correct vector file clicking **...** and browse directly to the file containing the training area polygons containing segments and features for the whole image **lahn-gi-spann-segments-meanshift-zonal.shp**.
* The name of the upper `input model` file is **lahn-gi-spann-obia.model**
* Output field containing the class is `CLASS_ID`
* Copy and paste into the field `Field names to be calculated` same attributes as above: `"mean_0 stdev_0 mean_1 stdev_1 mean_3 stdev_3"`
* Name the `output vector` data **lahn-gi-spann-classified_obia.shp**.
* Push `Run`.

{% include medium-img.html url="obia6-class.png" %}

Load the output vector file into QGIS and apply the same QGIS style used for the training data. `Layer->Layer properties->Symbology->Style->Load style...`.

