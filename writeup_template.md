# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve.jpg"

---

### Reflection

### 1. Describe your pipeline. 

My pipeline consisted of 9 steps. 

1. Convert the images to grayscale
2. Apply a slight Gaussian blur with kernel size of 5
3. Apply Canny edge detection of low and high threshold of 50 and 150. This setting was obtained from the lecture quiz, and works well on the given images and videos.
4. Next, apply a region of interest that is determined emperically based on the fix vantage point of the camera lens. 
5. Apply Hough transform to find lines within the region of interest. After this step, we've got a set of lines that potentially mark the left and right lanes
6. Filter out lines with absolute slope outside of the range [0.4, 1] which was determined emperically. Due to fixed camera position, the lanes tend to have slope confined to a small range.
7. Sort the lines into left or right lane based on their slopes: negative for left, positive for right.
8. Next, apply a linear regression separately on each lane to consolidate the lines in to a single line. 
9. Calculate the co-ordinate of 2 points on the consolidated line for each lane. Draw the lines and super-impose on the original image.

The results on the test images are given below (note: OpenCV uses reverse RGB channel representation):

![alt text][image1]

Result on video:
solidWhiteRight
[![solidWhiteRight](https://img.youtube.com/vi/OY2Jn0kOYJw/0.jpg)](https://www.youtube.com/watch?v=OY2Jn0kOYJw)

Optional challenge:
[![solidWhiteRight](https://img.youtube.com/vi/pijgtIqRyiQ/0.jpg)](https://www.youtube.com/watch?v=pijgtIqRyiQ)

### 2. Potential shortcomings with current pipeline

1. Many parameters set by hand and empirical experiments, e.g. Canny params, Hough transform params, not so much of automated learning from data.


### 3. Suggest possible improvements to your pipeline

1. Apply machine learning to learn parameter automatically, but this requires labelled data.
2. The heuristic almost works well for the challenge video, except for a few frames. For curvy roads, the pipeline could be further improved. 
