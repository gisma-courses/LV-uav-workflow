---
title: " Howto manually align and merge Chunks "
published: true
morea_id: experience-fw-20
morea_summary: "Align Metashape Chunks"
morea_url: 
morea_type: experience
morea_sort_order: 20
morea_labels:
 - preliminary 
 - knowledgebase

---

# Optimize Alignment: How to align and merge Chunks

It happens sometimes that not all pictures can be aligned. First, you can try to solve this situation by choosing different Alignment parameters, i.e. higher (or lower!) quality, or by adding georeference to the pictures (this way the Reference Preselection can be used). If this does not improve the result there is another method to get the not aligned pictures into the point cloud model. In general, you have to manually select the not aligned pictures in the point cloud model, move them into a new chunk, align them separately and then move them back into the main chunk and merge them into the point could.

Usually the not aligned pictures occur in groups so you can select a whole area using the selection tool. Most likely there are pictures around the unaligned areas that have been aligned. It is very important to include a reasonable amount of these aligned pictures (at least all neighboring pictures) into the selection. These additional pictures are later used to re-integrate the newly aligned segment into the main point cloud.

Re-integration is done in two steps: First, the two (or more) chunks are aligned and afterwards merged into one final chunk. Because of the necessary procedure (see work flow below) this will lead to a larger number of pictures in the main chunk. But the aim to have a more consistent and complete point cloud works quite well. Surplus pictures in the main chunk can be removed.

If the alignment does not improve enough you can still move a part of the not aligned pictures from the first separated chunk to another sub-set chunk. 
{% include note.html content="

Remember to align and merge the chunks “upwards” in the reverse direction you reduced them in the “downwards” selecting process.
"
%}


## General workflow

  1. Duplicate chunk
  1. Activate duplicated chunk and select not aligned pictures by using the selection tool including aligned pictures around them (work in the model window, not in the picture list!)
  1. Inverse selection and delete pictures (in the picture list!). The result should be a chunk with the not aligned pictures surrounded by some aligned pictures
  1. Delete the Tie Points in the new chunk. (Note: You can still see how many pictures were originally aligned. Remember this number to check if the new alignment improves the situation.)
  1. Align pictures in the new chunk, use the same parameters as before and adapt them if the results are not satisfying
  1. Now all chunks will be combined, first by aligning them. Use “Align Chunks” in the Workflow Menu. Here you can set parameters for the alignment similar to the picture alignment. Parameters for the best results depend on the situation of the pictures. [A good try: Method = Point based, Accuracy = Medium, Point Limit = 0]. 
  1. Finally merge the chunks. [Choose only those chunks you need, leave out “working chunks”!]
  1. Optional, the surplus (double) pictures can be removed to lower project file size.

## References for alignment optimizing

  * [Photoscan Manual](https://www.agisoft.com/pdf/metashape-pro_1_8_en.pdf)
  - [Search filter](https://www.agisoft.com/forum/index.php?action=search2;params=eJwtzTEOgzAMBdC7sLB4wGUot4mC8wVUIalMoKqUw9epWKz_ny3Zh8snQah95drVWVt6Ek_ETDYsDsQjPQbbHmv-OMn7O6LA7hqd8wtSXE7xe0vW4sKm1gIOucWaIuL_rBG8ymq4Q5ctLT9qwjF9)
  - [Merging Chunks](http://www.agisoft.com/forum/index.php?topic=6995.0)
  - [Chunks alignment](http://www.agisoft.com/forum/index.php?topic=148.0)
  - [Agisoft Tutorial: Marker based chunk alignment](http://downloads.agisoft.ru/pdf/PS_1.0.0_Tutorial%20(Intermediate%20level)%20-%20Marker%20Based%20Chunk%20Alignment.pdf)
  - [Chunks Workflow](http://www.agisoft.com/forum/index.php?topic=381.0)

