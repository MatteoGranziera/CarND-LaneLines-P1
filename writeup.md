# **Finding Lane Lines on the Road** 

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

My pipeline consisted of 6 steps:

- Step 1. Convert to grayscale the image

[Grayscale image][./examples/grayscale.jpg]

- Step 2. Apply gaussian blur

- Step 3. Find edges by canny alghorithm

[Canny image][./examples/canny_solidYellowLeft.jpg]

- Step 4. Remove all edges out of the region of interest
    NOTE: It's better remove useless edges after the canny algorithm in order to avoid edges caused by the mask of the region of interest
    
[Region image][./examples/region_solidYellowLeft.jpg]

- Step 5. Draw lane lines using Hough alghorithm

[Lanes image][./examples/lanes_solidYellowLeft.jpg]

- Step 6. Draw lanes on the original image

[Result image][./examples/result_solidYellowLeft.jpg]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by sperate hough lines in two sets, one for left lane and one for the right lane. The process also remove lines with the slope out of a specific tuned range and note the lenght and the lowest y position on the image for each line that will be used as weight for an average   coefficients calculation. In the end calculate lines vertices using an weighted average coefficients.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is too bright and the canny algorithm can't identify the edges on grayscale color space.

Another shortcoming could be cracks on the road that can be represented as edges and some cracks in right lane with left slope can change the slope of the left line. Obviously the same could happen for the righ lane


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use more than one color space to identify more edges and give more weight on lines that are present in more colorspaces.

Another potential improvement could be to split region of interest in two, one for each lane to identify better edges involved in each lane and exclude potential cracks on the road.
