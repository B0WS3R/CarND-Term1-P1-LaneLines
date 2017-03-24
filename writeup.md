#**Finding Lane Lines on the Road** 



#### Sebastian Lena 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./images/white_right_output.png "Solid white line on the right"
[image2]: ./images/yellow_left_output.png "Solid yellow line on the left"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

# The basic pipeline

####Algorithm description:

    1-  Calculate the regions of interest based on LEFT and RIGHT REGION_VERTEXES
    2-  With this regions, generate mask for each color (yellow and white), apply each of these masks to each interest zone,
        white for left and right (the same for the yellow mask)
    3-  Combine finals white and yellow masks into one mask, get -> final_mask
    4-  Apply a small gaussian blur to the final_mask, get -> blur_mask
    5-  Run Canny edge detection to detect edges and give a black and white image (from blur_mask), get -> edges
    6-  Perform slight dilatation on edges, get -> edges
    7-  Separate edges into two edges, left_edges and right_edges, both determined by a region_of_interest
    8-  Run a Hough transform on the edges (left and right), get -> left_lines && right_lines
    9-  Remove the lines that have an unacceptable slope, run a linear regression once on the left && once on the right
    10- Use y = mx + c to calculate extreme point for each lane, with the get values from linear regression now we can
        extrapolate (final lanes)
    11- Draw the lane lines 

(please view the .pynb)

### Image references (pipeline process)

####Output 1: Solid white right line 
![alt text][image1]

####Output 1: Solid yellow left line
![alt text][image2]



###2. Identify potential shortcomings with your current pipeline

####Some defects of this implementation would be:

- Faster light chances
- Curves

These situations would cause the pipeline algorithm to fail.


###3. Suggest possible improvements to your pipeline

####A possible improvement would be:

- Keep a memory about lines so when they missing, I can use prior knowledge to draw them correctly.
- Improve and increase the color boundaries range (in this case yellow and white). I think this will make the algorithm more robust to light changes.

###External references
 
- I took some notes from http://flippidybits.com/ about extrapolation.
- From http://www.pyimagesearch.com/ about masking.

Thanks.

    