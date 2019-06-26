# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/writeUp/01-gray.jpg "Grayscale"
[image2]: ./test_images_output/writeUp/02-blur_gray.jpg "Blur Grayscale"
[image3]: ./test_images_output/writeUp/03-edges.jpg "Edges"
[image4]: ./test_images_output/writeUp/04-edges_white_yellow.jpg "Edges + White + Yellow"
[image5]: ./test_images_output/writeUp/05-lines_edges.jpg "Detected Lines"
---

### Reflection

### 1. Pipeline (code) description

My pipeline consisted of 5 steps: 

1. I converted the images to grayscale, then using a Gaussian smoothing method, I can provide a gray image with a low amount of Gaussian noises.

![alt text][image1]

![alt text][image2]

The second step is to find edges. For this, I used Canny edge detection method.   

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

