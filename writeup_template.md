# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of seven(7) steps: 

First, I converted the images to grayscale, then I blurred the images using the CV2 gaussian blur function (kernel_size=11) 
to smooth out the rough edges for the lines in the images. Next, I found the canny edges for pixel gradients with low_threshold=75 and high_threshold=150.  
Fourth, I worked out a region of interest in the video stream to narrow in on the left and right lanes on the road.  From the region of interest 
in the video frames I created a masked images that showed the canny edges.  

Fifth, I calculated the Probabilistic Hough Transforms on the canny edges using parameters: 
rho=1, theta=np.pi/180, threshold=30 , min_line_len=15, max_line_gap=5.  The Hough parameters were found by trial and error.  
They helped filter out objects that were not related to lane lines like: trash in the road, others cars, road reflectors, 
and stray markings on the roads.  Also, they helped to filter out lane markings which were not suitable for further processing.  

Sixth, using the hough lines I split them into left and right lines corresponding to left lane and right lane lines.  
From the lines I drew left and right road lanes on the masked images.  

My draw_lines() function consisted of three methods: 

	(1) default: using the cv2.line() function with the raw (x,y) points from the Hough Lines. 
	(2) using linear regression to find the slopes and intercepts from the raw (x,y) points
	(3) using a weighted average of slope and intercepts from the raw (x,y) points.

I wanted to extrapolate the line data to draw solid lane lines on the roads so I used (2) and (3) to do that.
I found that (3) the weighted average approach gave the most stable lines probably because it gave more weight to longer 
(and more credible) lines rather than giving equal weight to each point in (2) the linear regression approach.

Seventh, and finally, I overlayed the lane lines onto the original; frame images using the cv2.addWeighted() function.

Here is an example of the pipeline in images:

![alt text][/test_video_output/1_1_image.jpg]
![alt text][1_2_gray_image.jpg]
![alt text][1_3_blurred_image.jpg]
![alt text][1_4_canny_image.jpg]
![alt text][1_5_masked_image.jpg]
![alt text][1_6_line_img.jpg]
![alt text][1_7_overlay_image.jpg]

Finally, here are the full videos with the pipeline applied.

White Markings:

![alt text][solidWhiteRight_1-30-15-5-3.mp4]

Yellow Markings:

![alt text][solidWhiteRight_1-30-15-5-3.mp4]

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
