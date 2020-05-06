# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg 
[image2]: ./test_images_output/solidWhiteRight.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps: 
1. First, I converted the images to grayscale, 
2. Then I found the edges in the pictures by using canny image detection.
3. After finding edges i used gaussian blur function to smooth ou the edges.
4. Then I masked out the image that is outside the region of interest(given by vertices) by using cv2.fillPoly() and cv2.bitwise_and.
5. After that I applied Hough Transform on the masked image.
6. At last i merged the line image with the original image by addWeighted method.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating line segments by their 
slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.  Then, I average the position of each of 
the lines and extrapolate to the top and bottom of the lane.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Example][image1]
![Example][image2]



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when dealing with no clear picture (shadows, light reflection etc. over a longer period => orientation at other edges) 

Another shortcoming is that image dimensions were hard-coded in at least one case.

Similarly If the lane lines are not straight lines but have high curvature, this algorithm may give weird results.



### 3. Suggest possible improvements to your pipeline

Tune parameters more systematically with more test images instead of by 'feel'.

Instead of forming lines we should form non-linear lines using hough transform.  
