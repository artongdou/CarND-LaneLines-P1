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

My pipeline consists of the following steps:
1) Convert image to grayscale and apply guassican blur to the image to reduce some of the noise.
2) Feed the filtered image into Canny edge detector and turns the image into white edges on black background.
3) Define the area of interests using vertices and mask edges detected outside of the image
4) Feed the masked image into Hough lines detector to extract the lines segments on the lane marker

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by dividing the line segments into 2 groups based on the slope. Negative slope corresponds to left lane and positive to right lane. And then I apply a 1D polyfit to each of the group. After the first polyfit, examine the fitting error and exclude those outside of the tolerance range. And then fit the rest of the segments in that group a second time to a straight line. Now that we have two fitted line. All we need to find out is the corresponding x value at the top and bottom of the area of interest. 

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![][./test_images_output/solidYellowCurve.jpg]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be when the vehicle is in a tight curve. In that case the pipeline might not accurately detect the lane because in the image the lane markers are not as straight anymore.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to fit a curve line instead of a straight line to track the lane marker.
