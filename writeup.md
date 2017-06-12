# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps. 

1. Filter the color to pickup yellow or white areas from the origin image
1. Transform the image into a grayscale image
1. Blur the image
1. Recongnize the edges
1. Extract the potential edges from the intrest area
1. Extract all hough lines
1. Transform hough lines into line border with hisotry parameters
1. Draw lane borders

#### The way the border's paramters are culculated

1. Assume the left border is on the left side of the image with a negative slope of which the value should be less then -0.5, while the right border should alway on the right side of the image with a positive slope of which the value should be grater then -0.5
1. Skip lines which are not meet the hypothesis above (treat them as outliners)
1. Assume short lines will give a smaller impact then longer ones in determine the parameters of lane border
1. Culculate the weighted arithmetic mean of slops and biases for left line group and right line group separately, while each line's length's square is the weight in culculating
1. Now we get the parameters of each border line based on this frame (image), then I merged the parameters from the last frame with a big weight to reduce the changes between 2 frames in order to reduce the　bad effect of the incidental low recognation accuracy in this frame. That is beacause I belive the lane line will not be changed in a extremely short time such as `1/30s`


### 2. Identify potential shortcomings with your current pipeline
1. It cannot recognize lines with colors other than yellow and white
1. Area of intrest is norrow, so it may miss some information when the lane is broader or the car is climing a slope
1. I just assume the lane is almost straight, if the lane curves in a short distance it may not works well


### 3. Suggest possible improvements to your pipeline
1. Use a color list to filter
1. Adjust the intrest area based on the information (amont of lines)
1. Seperate the line into several part and culculate the parameters for each part
