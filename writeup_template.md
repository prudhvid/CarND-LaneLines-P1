**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[solidWhiteCurve]: ./test_images/solidWhiteCurve.jpg "SolidWhiteCurve"
[solidWhiteCurve_grayscale]: ./test_images_output/grayscale_solidWhiteCurve.jpg "solidWhiteCurve_grayscale"
[solidWhiteCurve_gaussian_blur]: ./test_images_output/gaussian_blur_solidWhiteCurve.jpg "solidWhiteCurve_gaussian_blur"
[solidWhiteCurve_canny]: ./test_images_output/canny_solidWhiteCurve.jpg "SolidWhiteCurve_canny"
[solidWhiteCurve_region_of_interest]: ./test_images_output/region_of_interest_solidWhiteCurve.jpg "SolidWhiteCurve_region_of_interest"
[solidWhiteCurve_weighted_image]: ./test_images_output/weighted_img_solidWhiteCurve.jpg "SolidWhiteCurve_weighted_image"

---

### Reflection

### 1. Pipeline
**My pipeline consisted of 5 steps**
1. First I changed to grayscale image using the standard cv function
2. Then I applied guassian blur with kernel 3
3. Then I detected edges using canny with threshold levels 50 and 150
4. After this, I've masked the image using region_of_interest method
5. Then obtained the lines using hough_lines
6. Drew the lines and returned the weighted_img

### 2. draw_lines() function
**In order to draw a single line on the left and right lanes, I modified the draw_lines() function by**
1. Seperate the left and right lines by the sign of slopes
2. Now, take the mean and std deviation of slopes for both the set of lines
3. Ignore all the lines that have slopes with error greater than std deviation, when compared to the mean
4. Take the mean of the slopes that were left for both the sets
5. Take the coordinates of the maximum length line and extrapolate them
6. Draw the lines thus obtained!


If you'd like to include images to show how the pipeline works, here is how to include an image: 

#### 1. Original Image
![SolidWhiteCurve][solidWhiteCurve]

#### 2. Greyscale
![solidWhiteCurve_grayscale][solidWhiteCurve_grayscale]
#### 3. Gaussian Blur
![solidWhiteCurve_gaussian_blur][solidWhiteCurve_gaussian_blur]
#### 4. Canny
![solidWhiteCurve_canny][solidWhiteCurve_canny]
#### 5. Masking
![solidWhiteCurve_region_of_interest][solidWhiteCurve_region_of_interest]
#### 6. Final Weighted Image
1. The light blue lines  - detected from hough_lines
2. The red line - drawn from draw_lines function

![solidWhiteCurve_weighted_image][solidWhiteCurve_weighted_image]



###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when ... 
When there is no line detected by the hough_lines function, then my algorithm will not draw any line at all
Another shortcoming could be ...
Flickering. It is more when compared to the video that was given in example

###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...
Taking color into consideration. This should be necessary for the challenge video

Another potential improvement could be to ...
To reduce Flickering, tried the following,
1. Take the maximum length line instead of means and standard deviations
2. Re-run the hough_lines method on the obtained lines and then increase the max_line_gap parameter to obtain larger lines

Both the appraches failed, I think one possible thing is to use previous history to make it stable