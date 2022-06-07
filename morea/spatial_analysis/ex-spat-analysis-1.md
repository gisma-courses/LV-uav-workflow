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


---

# Object-based image analysis (OBIA) 

Human visual perception almost always outperforms computer image processing algorithms, For example, your brain knows a river when it sees one. But a computer can't distinguish rivers from lakes, roads or sewage treatment plants.

Especially with the spatially extreme and spectrally minimal resolution UAV image data, a change in thinking must take place. It makes more sense to think in terms of objects or entities to be identified rather than classifying in terms of individual pixels. The basic principle of object-based image analysis (OBIA) is to segment first and then classify.

The segementation process is algorithm-dependent but looks iteratively for similarities in space, structure and channel dimensions for grouping neighboring and similar pixels into objects. This segements are clasiefied in a next step using supervised training data.
 

<br>
# The complete OBIA Workflow in a YouTube nutshell
<br>
{% include youtube.html id="fX2UpOwoYLk" %}
<br>
# Step by step

### Step-1 Create Training Sample Points by manual digitizing 

You may follow this [instructions](https://geomoer.github.io/geoAI//unit02/unit02-03_digitize_training_areas.html). However we just digitize Points and not areas (polygons). In addition you may <a href="obia.zip" >Download</a> the basic data.

{% include note.html content="<br>
 Activate under `Main Menu->Settings->Digitize` and check *`Reuse last entered attribute values`*. this will makes in much more comfartable to digitize training points of one class in series.
"%}


Create a point vector file and digitize the following classes:

|class| CLASS_ID|
|:-- | --:|
|water|1|
|meadows|2|
|meadows-rich|3|
|bare-soil-dry|4|
|crop|5|
|green-trees-shrubs|6|
|dead-wood|7|
|other|8|


Provide at minimum 10 widely spred sampling points.

Save this file naming it `sample.shp`.

### Step-2 Segmentation

In the search field of the `Processing Toolbox`, type *segmentation* and double click `Segmentation`.

* select the `input image`: **example-5.tif**
* select `meanshift` from the drop-down list **Segmentation algorithm**
* The `Spatial Radius` value can be set to **25**.This is determining the spatial range of the segementation and is also experimental. Try to identify the scale of your major classes in pixel.
* The `Range Radius` value can be set to **25**. We are dealing with RGB images that have a range `0-255`. The optimal value depends on datatype dynamic range of the input image and requires experimental trials for the specific classification objectives.
* Set `Minimum Region size` in pixels to **25**. Minimum size of a region (in pixel unit) in segmentation. Smaller clusters will be merged to the neighboring cluster with the closest radiometry.
* keep `Processing mode`  as **Vector**
* Tick `8-neighborhood connectivity` on.
* Set `Minimum object size` in pixels to **200** 
* Name the `Output vector file`  as  **segments-meanshift.shp**. 
* Push `Run`.
<br>
{% include medium-img.html url="obia1.png" %} 
<br>

**Evaluate the segmentation results:**

* Load the output vector file **segments-meanshift.shp** into your QGIS session and place it on top of the image **example-5.tif**
* Colorize the vector layer in the QGIS Layers window. Right click `Properties->Symbology->Simple Fill`, `Fill Style`: `No Brush` and `Stroke color`: `white`.

###  Step-3 Feature extraction 
Type `zonalstats` in the search field of the Processing Toolbox and open `ZonalStatistics` which is settled under the image manipulation section of OTB.

* Select as input image: **example-5.tif**.
* Select `input vector data` the vector file with segments from above segmentation **segments-meanshift.shp**
* Name for the `output vector`: **segments-meanshift-zonal.shp**.
* Push `Run`.
<br>
{% include small-img.html url="obia2-zonal.png" %} 
<br>


## Step-4 Joining training data with segements

In the search field of the `Processing Toolbox`, type *join* and double click `Join Attributes by Location`.

* select the `Base Layer`: **segments-meanshift-zonal.shp**
* select the `Join Layer`: **sample.shp**
* `Join Type`: choose **Take Attributes of the first matching...**
* Tick `Discard records which could not be joined`
* Provide an output filename
<br>
{% include small-img.html url="obia3-join.png" %} 
<br>
{% include note.html content="
Sometimes the geometry is broken. Type `fix` in the search field of the Processing Toolbox and open `Fix Geometries` which will in most cases do the job
"%}


###  Step-5 Training
Type `train` in the search field of the Processing Toolbox and open `TrainVectorClassifier`

* In the  field  `Vector Data List` select  the correct vector file clicking **...** and browse directly to the file containing the training area polygons **segments-meanshift-zonal.shp**.
* Provide the `Output model filename` as **lahn-gi-spann-obia.model**
* In the field `Field names for training features` copy and paste `"mean_0 stdev_0 mean_1 stdev_1 mean_3 stdev_3 mean_2 stdev_2"`
* The name of `Field containing the class id for supervision` is `CLASS_ID`.
* Classifier to use for training: `libsvm` Usually the straighforward Support Vector Machine is doing a good job. 
* SVM Kernel Type: `linear`
* SVM Model Type: `csvc`
* tick `Parameters optimization` to `ON`.
* Push `Run`
<br>
{% include small-img.html url="obia5-train.png" %} 
<br>

###  Step-6 Classification 
Type `class` in the search field of the Processing Toolbox and open `VectorClassifier`
*  In the  field  `Vector Data` select *manually** the correct vector file clicking **...** and browse directly to the file containing the training area polygons containing segments and features for the whole image **lahn-gi-spann-segments-meanshift-zonal.shp**.
* The name of the upper `input model` file is **lahn-gi-spann-obia.model**
* Output field containing the class is `CLASS_ID`
* Copy and paste into the field `Field names to be calculated` same attributes as above: `"mean_0 stdev_0 mean_1 stdev_1 mean_3 stdev_3 mean_2 stdev_2"`
* Name the `output vector` data **lahn-gi-spann-classified_obia.shp**.
* Push `Run`.

Finally load the output vector file into QGIS and apply the same QGIS style used for the training data. `Layer->Layer properties->Symbology->Style->Load style...`.

<br>
{% include small-img-two.html url1="obia6-class.png" url2="classification.png" %}
<br>

You will see partly predominantly excellent classification. However, there are also significant misclassifications. What could be the reason for that. What is a weakness of this approach?