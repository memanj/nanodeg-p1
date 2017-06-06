# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/region_interest.jpg "Region of interest for lane finding"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows.
First, I converted the images to grayscale, then applied gaussian blur to further smoothen the edges. This smoothed image was run using canny method using minmum and maximum threshold values discussed in the quiz.

Once the canny edges are detected, vertices of the polygon are choosen in such a way that the lanes fit inside the polygon. Using fillpoly function the detected points for the lines are represented as masked edges.

![alt text][image2]

The masked edges are then used to generate hough lines. Which return a list of lists of x, y co-ordinate pair for the hough lines.

Important observations made:
- After going the entrire test images and test videos. I figured out that threshold is the most important parameter for hough function, as too small a value would result in wrong slope for the extrapolated line.
- Spent a lot of time figuring out the extrapolation algorithm, I was able to come closer to the solution but could not optimize it to get the desired result. Later figured from the forums that python already has inbuilt functions for this. 
If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
