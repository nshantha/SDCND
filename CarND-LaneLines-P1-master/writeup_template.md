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

My pipeline consisted of same steps that was performed in previous assignments.

First, I converted the images to grayscale, then I applied gaussian blur to smoothen and reduce noise, then generated
Canny edges from the grayscaled image, then generated region of interest by defining vertices of region. After obtaining the 
ROI, I performed Hough transform to obtain hough lines on the ROI, then drew the obtained hough lines on the input image.

When the obtained hough lines were drawn onto the image, the lines were not fully constructed. Thus, averaging out the lines and extrapolating then after obtaining hough lines proved to be important.

I was not familiar as to which extrapolation technique had to be used. Using https://medium.com/@mrhwick/simple-lane-detection-with-opencv-bfeb6ae54ec0 as reference explained how the concept to implement the following technique which I used.

I modified the draw_lines function for averaging and extrapolating. I obtained the slope using the slope formula by using seperate co-ordinates of the respective position of the lines by seperating co-ordinates of each slope obtained and ignoring small slope values. To obtain the best co-efficients possible, numpy's least square polynomial fit, polyfit function was used to fit values accordingly.
To generate linear equation of the lines of obtaining a linear 1-D polynomial class, poly1D function of numpy was used. After obtaining the respective values, I used OpenCV to draw lines on each frame of the image. This method provided better constructed lines to analyse the lines for cars.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are intersection and multiple white lines in intersection where this method would not work. 
As this detect white lines, any possible interferece with the lines, with anything white can interfere with the algorithm.
This method cannot be used outside highways, like country roads and trails.
This method also does not allow for more robust solutions of finding lines in various climate conditions.


### 3. Suggest possible improvements to your pipeline

Improvements for this would be to use different case scenarios with multiple tuning for the above mentioned cases like traffic simulation, climate and intersection updation.

