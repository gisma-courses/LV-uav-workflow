---
title: "OBIA Workflow for QGIS in a nutshell"
toc: true
toc_label: Inhalt
published: true
morea_id: ex-spat-analysis-0
morea_summary: "The basic Object-based image analysis (OBIA) workflow with QGIS and the OTB processing plugin follows a straightforward approach. This Video shows a very common way."
morea_url: 
morea_type: experience
morea_sort_order: 11
morea_labels:
 - basic
 - mandatory 
 - YouTube 18min


---

# Object-based image analysis (OBIA) 

Human visual perception almost always outperforms computer image processing algorithms. For example, your brain knows a river when it sees one. But a computer can't distinguish rivers from lakes, roads, or sewage treatment plants.

Especially with the spatially extreme and spectrally minimal resolution UAV image data, a change in thinking must take place. It makes more sense to think in terms of objects or entities to be identified rather than classifying them in terms of individual pixels. The basic principle of object-based image analysis (OBIA) is to segment first and then classify.

The segmentation process is algorithm-dependent but looks iteratively for similarities in space, structure, and channel dimensions for grouping neighboring and similar pixels into objects. These segments are classified in the next step using supervised training data.


#### The complete OBIA Workflow in a YouTube nutshell

For all who prefer the workflow as video.

<br>
{% include youtube.html id="fX2UpOwoYLk" %}
<br>
