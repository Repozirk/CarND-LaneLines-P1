# **Finding Lane Lines on the Road** 
[image1]: ./test_images/solidWhiteCurve.jpg 
[image2]: ./test_images/graysolidWhiteCurve.jpg 
[image3]: ./test_images/cannysolidWhiteCurve.jpg 
[image4]: ./test_images/areasolidWhiteCurve.jpg 
[image5]: ./test_images/maskedsolidWhiteCurve.jpg 
[image6]: ./test_images/houghsolidWhiteCurve.jpg 
[image7]: ./test_images/solidsolidWhiteCurve.jpg 

## Reflection
My pipeline consisted of 10 steps:

### This is the original image:
[image1]: ./test_images/solidWhiteCurve.jpg 
![alt text][image1]

### Step1: Convert the image to greyscale
[image2]: ./test_images/graysolidWhiteCurve.jpg 
![alt text][image2]

### Step2: Run Gaussian Smoothing and CannyEdgeDetection
[image3]: ./test_images/cannysolidWhiteCurve.jpg 
![alt text][image3]

### Step3: Define the area of interest
[image4]: ./test_images/areasolidWhiteCurve.jpg
![alt text][image4]

[image5]: ./test_images/maskedsolidWhiteCurve.jpg 
![alt text][image5]

### Step4: Run Hough Transformation
[image6]: ./test_images/houghsolidWhiteCurve.jpg 
![alt text][image6]

### Step5: Draw the Hough lines on the image
Just drawing all lines from Hough Transformation over the orignal image

### Step6: Separate lines with positive and negative slopes
For the goal to get 2 solid lines it was necessary to seperate the lines form Hough by ther slope
Therefor the helper functions grad_pos_calc(lines) and grad_neg_calc(lines) have been created.
Output: List with the x and y values for the pos and neg slopes.

### Step6: Restrict the min and max possible gradients/slopes
This helper function restrict_grad(grad, grad_max_thd, grad_min_thd) collected all x and y values for lines with a slope within the boundaries grad_max_thd and grad_min_thd
Output: List with the x and y values for the restricted pos and neg slopes.

### Step7: Collecting all x1/x2 and y1/y2 for pos and neg restricted gradients/slopes
Just put all teh x1 and x2 values in 1 column and all the y1 and y2 values in another column with helper function all_val_one_lst(data). That is necessary for further processing
Output: List with all x and y values in 2 column 

### Step7:Run the fittin line process
This part of the pipeline creates the data for the solid lines depending on the results out of Hough Transformation and further slope/gradient speration and restriction.
With the helper function 


## 2. Identify potential shortcomings with your current pipeline





## 3. Suggest possible improvements to your pipeline


