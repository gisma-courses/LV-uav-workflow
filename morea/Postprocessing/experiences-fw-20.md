---
title: " Howto manually align and merge Chunks "
published: false
morea_id: experience-fw-20
morea_summary: "Align Metashape Chunks"
morea_url: 
morea_type: experience
morea_sort_order: 20
morea_labels:
 - supplement
 - hands on

---

# Optimize Alignment: How to Align and Merge Chunks

Sometimes, not all images can be aligned during processing. To address this, try adjusting the alignment parameters — for example, by increasing (or decreasing!) the alignment quality, or by adding georeference data to the images (this allows you to use Reference Preselection).  
If these measures do not improve the result, there is another approach to incorporate the unaligned images into the point cloud model.

In general, you must manually select the unaligned images in the point cloud model, move them into a new chunk, align them separately, and then re-integrate them into the main chunk by aligning and merging the chunks.

Typically, unaligned images appear in groups. Use the selection tool to select the entire affected area. Be sure to include surrounding, **already aligned** images in your selection — especially all neighboring images. These surrounding images are critical later when reintegrating the newly aligned chunk into the main point cloud.

Reintegration involves two main steps:  
1. **Aligning the chunks**  
2. **Merging them into a single final chunk**  

Due to this process (outlined below), the number of images in the main chunk may increase. However, the goal — a more consistent and complete point cloud — is generally well achieved. Surplus images in the final chunk can be removed to reduce file size.

If alignment quality is still unsatisfactory, you may split the original unaligned chunk into smaller subsets for further refinement.

{% include note.html content="
Remember to align and merge the chunks *upwards*, in the reverse order of how you split them during the *downwards* selection process.
" %}


## General Workflow

1. **Duplicate the chunk.**  
2. **Activate the duplicated chunk** and use the selection tool in the 3D model window (not in the image list) to select the unaligned images, including all neighboring aligned images.  
3. **Inverse the selection** and delete the deselected images from the image list. The resulting chunk should now contain only the unaligned images and their immediate aligned neighbors.  
4. **Delete the Tie Points** in this new chunk. *(Tip: Note the original number of aligned images so you can later assess whether the new alignment improved.)*  
5. **Align the images** in the new chunk, using the same parameters as before. Adjust them if necessary to improve results.  
6. **Align all chunks together** using the “Align Chunks” option in the Workflow menu. Set alignment parameters similar to those for photo alignment. *(Good starting parameters: Method = Point Based, Accuracy = Medium, Point Limit = 0)*  
7. **Merge the chunks.** Be sure to include only the relevant chunks and exclude temporary “working chunks.”  
8. **(Optional)**: Remove any surplus (duplicate) images to reduce project size.


## References for Alignment Optimization

- [Metashape Manual](https://www.agisoft.com/pdf/metashape-pro_1_8_en.pdf)  
- [Search Filter](https://www.agisoft.com/forum/index.php?action=search2;params=eJwtzTEOgzAMBdC7sLB4wGUot4mC8wVUIalMoKqUw9epWKz_ny3Zh8snQah95drVWVt6Ek_ETDYsDsQjPQbbHmv-OMn7O6LA7hqd8wtSXE7xe0vW4sKm1gIOucWaIuL_rBG8ymq4Q5ctLT9qwjF9)  
- [Merging Chunks](http://www.agisoft.com/forum/index.php?topic=6995.0)  
- [Chunks Alignment](http://www.agisoft.com/forum/index.php?topic=148.0)  
- [Chunks Workflow](http://www.agisoft.com/forum/index.php?topic=381.0)
