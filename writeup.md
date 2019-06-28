# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./test_images_output/writeUp/01-gray.jpg "Grayscale"
[image2]: ./test_images_output/writeUp/02-blur_gray.jpg "BlurGrayscale"
[image3]: ./test_images_output/writeUp/03-edges.jpg "Edges"
[image4]: ./test_images_output/writeUp/04-edges_white_yellow.jpg "Edges_White_Yellow"
[image5]: ./test_images_output/writeUp/05-lines_edges.jpg "Detected_Lines"

---

### Reflection

### 1. Pipeline (code) description

My pipeline consisted of 5 steps: 

1. I converted the images to grayscale, then using a Gaussian smoothing method, I can provide a gray image with a low amount of Gaussian noises.

Grayscale

![alt text][image1]

Blurred Grayscale with kernel_size = 3

![alt text][image2]


2. The second step is to find edges. For this, I used Canny edge detection method. I chose these values for Canny filter:

low_threshold  = 50

high_threshold = 150

And, this is the output:

Canny Edges

![alt text][image3]


3. These results are good but we can improve it by adding the white and yellow points information. But, how?
I propose the following method to extract the white and yellow points that we need to add the edges result:

#### white color info  --> provided by gray scale image (using graymask function in lane_line_detector.ipynb)
For white color info, the gray scale image works better than the HSV scale and has lower artifacts.

#### yellow color info --> provided by HSV scale image (using hsvmask function in lane_line_detector.ipynb)
For yellow color info, the HSV scale image works better than the gray scale and has lower artifacts.

This is the result of combined edges and white-yellow info (please check lane_line_detector.ipynb for more information):

Edges + White + Yellow

![alt text][image4]

4. Next, we'll create a masked edges image to define the region of interest. For my case the region of interest is a trapezoid to include the part of road that the car moves forward straightly.


5-6. Hough transformation and drawing line
For obtaining the lines based on the last step results, I used the Hough transform. After that, I draw the lines using the draw_lines() function which meet my conditions. 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by considering the slope of detected lines. Then, select the slopes in a specific range and continue with finding the left and right lines based on the slope value and geometry. Then, in each category, do the interpolation by the numpy polyfit function and fit a line for each category (i.e. one for left and one for right category). Using this simple equation, y = m*x + b --> x = (y - b)/m, and knowing the 'y' values for the region of interest and 'm' and 'b' from the previous step, we can extrapolate the detected left and right lines to cover all the region of interest. 

This is he final result obtained by my proposed method:

Detected Lines

![alt text][image5]

### 2. The potential shortcomings with my current pipeline


One potential shortcoming would be what would happen when the road condition in not good/normal. For example in the case of fog, snow, rain, and snow. In these cases, the current pipeline will face difficulties to detect the markers in camera images. 

Another shortcoming could be about the false detection and how can we make the car to avoid the accident. For example if there is a network problem in camera and local pc communication which makes the the current code can not detect the lines correctly.


### 3. Possible improvements to my pipeline

A possible improvement would be to add other markers to code to detect the main boundaries of the road. For example, consider a new region for detecting main boundaries. Also we need to avoid the obstacles like cars. We can do this by considering other sensor date like lidar.

Another potential improvement could be by changing the source codes to c++ in other to detect faster(live) which is necessary for cars situation in real world.

