[//]: # (Image References)
[image1]: ./examples/hog-visualization.png
[image2]: ./examples/detection-img1.png
[image3]: ./examples/detection-img2.png
[image4]: ./examples/detection-img4.png
[image5]: ./examples/detection-img5.png
[image6]: ./examples/heatmap.png
[image7]: ./examples/threshold.png
[image8]: ./examples/heatmap1.png
[image9]: ./examples/heatmap2.png
[image10]: ./examples/heatmap3.png
[image811]: ./examples/heatmap4.png
[image12]: ./examples/heatmap5.png
[image13]: ./examples/heatmap6.png

[video1]: ./project_video_out.mp4



### Histogram of Oriented Gradients (HOG)

#### 1. After reading the training images I am getting the HOG features in the 6th code block in my notebook. The code is mainly from the lesson materials.  

 
Here are some example of the training images
![alt text][image1]




#### 2. Explain how you settled on your final choice of HOG parameters.

I tried various combinations and found the following setup worked the best for me. 

* color_space = 'LUV' # Can be RGB, HSV, LUV, HLS, YUV, YCrCb
* orient = 9 # HOG orientations
* pix_per_cell = 8 # HOG pixels per cell
* cell_per_block = 2 # HOG cells per block
* hog_channel = 0 # Can be 0, 1, 2, or "ALL"
* spatial_size = (32, 32) # Spatial binning dimensions
* hist_bins = 8 # Number of histogram bins
* do_spatial = 1 # Spatial features on or off
* do_hist = 1 # Histogram features on or off
* do_hog = 1 # HOG features on or off
* y_start_stop = [None, None] # Min and max in y to search in slide_window()
* spatial_feat=True 
* hist_feat=True 
* hog_feat=True


#### 3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

I followed the couse material and trained a Linear Support Vector Classification (SVC) with the training images. This code is in section #3 of my notebook. 2% of the data was randomly separated for testing.   

### Sliding Window Search

#### 1. Implementation of sliding window follows the course lectures. I implemented a prospective view where used I used 128x128 pixels closer cars and 32x32 pixels for cars away from me. Sliding window function alone with other helper functions like bin_spatial and color_host are listed under the Image features sections.



#### 2. Some examples of test images to demonstrate the pipeline is working.  
One of the major optimization I did was to augment the training data set by flipping each image. I tried different configurations and settling on LUV channel and HOG channel 0. 

Here are some example of my pipeline
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]

---

### Video Implementation

#### 1. Here's a [link to my video result](./project_video_out.mp4)


#### 2. Filter for false positives and method for combining overlapping bounding boxes.

In my pipeline method, I am using a list to keep track of all the rectrangles for last 5 frames. I am using rectangles from previous frames along with the current frame to generate the heat map. Then I pass the heat map through threshold and labels to identify the cars. Onec the cars have been identified I am using the draw_labeled_bboxes method to draw boxes around the cars. 

### Here is a test image with corresponding heatmaps and threshold:

![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]

### Here is the output of `scipy.ndimage.measurements.label()` on the integrated heatmap from all six frames:
![alt text][image8]
![alt text][image9]
![alt text][image10]
![alt text][image11]
![alt text][image12]
![alt text][image13]

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

I am still having lots of false positive.  I think if I train my model with more data and I may get a better result.  Also, I my filter for removing false positive is not very good. I need to improve my filter to filter out more false posivitives. 
