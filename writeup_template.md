# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/region_interest.jpg "Region of interest for lane finding"
[image3]: ./examples/hough_transform.png "Hough Transform"
[image4]: ./examples/error_detection.png "Error in lane detection"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

First, I converted the images to grayscale, then applied gaussian blur to further smoothen the edges. This smoothed image was run through canny edge detection using minmum and maximum threshold values discussed in the quiz.

Once the canny edges are detected, vertices of the polygon are choosen in such a way that the lanes fit inside the polygon. Using fillpoly function the detected points for the lines are represented as masked edges(in red).

![alt text][image2]

The masked edges are then used to generate hough lines. Which return a list of lists of x, y co-ordinate pair for the hough lines.
![alt text][image3]

In order to draw a generate a line for the left and right lanes, I modified the draw_lines() function as follows.
1) Calculate the slopes of all the hough lines and since we already know that these lines are part of the lane lines. Separate these lines based on the slopes. Slopes are considered because based on the position of the camera at the top of the car. The lanes will always converge towards.
2) Slope for left is negative since the Y-aixs is inverted for our image axis. Similarly right lane has positive slope.
3) Then accummulate all the x and y co-ordinates separately for left and right lanes. Initially I was working on a extrapolation algorithm.
4) Once we have this, the points can be extrapolated to a line formed by these points using polyfit method of degree 1(since we are looking for a line). Equation y=mx+b can be generate by numpy module poly1d.
5) Using the equation we can generate two points for left and right lane lines by using the x-coordinate.
6) Lines are overlayed eventually based on the these two points on the line to be displayed for the final result.


Important observations made:
- After going the entrire test images and test videos. I figured out that threshold is the most important parameter for hough function, as too small a value would result in wrong slope for the extrapolated line.
- Spent a lot of time figuring out the extrapolation algorithm, I was able to come closer to the solution but could not optimize it to get the desired result. Later figured from the forums that python already has inbuilt functions for this. 

### 2. Identify potential shortcomings with your current pipeline


Below are some of the issues with this logic:
1) Co-ordinates for the polygon are fixed, in real time the lanes are changing dynamically every moment
2) Lanes cannot always be straight lines
3) In the example videos there are no vehicles in the lane considered, which very unlikely


### 3. Suggest possible improvements to your pipeline

Below are some of the improvements I think of in the pipeline
1) Parameters for Hough lines can be adapted dynamically using some sort of feeback loop 
2) One of the bug I found was the lane detection doesn't work for the entire duration of the video. Still working on fixing this issue.
![alt text][image4]
