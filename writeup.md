# **Finding Lane Lines on the Road** 


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
1. I converted the images to grayscale
2. I applied Gaussian Blur with a kernel size of 5. Indeed the road lines are so large so we can go above 3
3. I then used a polygon (trapezoidal) mask
4. I applied the probabilistic Hough tranform with the settings that we saw in the previous quiz
5. I then drew the resulting line segments with the draw_lines() function

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. computing the slopes of the line segments resulting from the Hough transform
2. filtering out the ones that were not between 0.4 and 0.9 (candidate for the right line) or -0.9 and -0.4 (candidate for the left line)
3. I averaged the coordinates of the left line candidates, same thing for the right line candidates
4. I then computed the coordinates of the two intersection points of a. the bottom line of the picture b. the upper limit of the trapezoidal mask
5. the two resulting lines are my approximation of the left and right line!


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the road is not straight, ie when we meet a turn. Then the Hough transform will fail, as it searches for *straight* lines.

Another shortcoming could be the height of the trapezoidal mask. If the car is climbing a moutain road, then the road will sometimes "fill the screen".


### 3. Suggest possible improvements to your pipeline

- a possible improvement would be to use the Generalised Hough transform, to search for curved lines and not only straight ones.
- we could also connect the various (straight) line segments, for example with the Numpy polyfit function
- we could remove outliers, before computing the interception points
- another potential improvement could be to use more complex techniques, as neural networks.
