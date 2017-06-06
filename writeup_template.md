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

### Step5: Draw the Hough lines on the image
Just drawing all lines from Hough Transformation over the orignal image
[image6]: ./test_images/houghsolidWhiteCurve.jpg 
![alt text][image6]

### Step6: Separate lines with positive and negative slopes
For the goal to get 2 solid lines it was necessary to seperate the lines form Hough by ther slope.
Therefor the helper functions grad_pos_calc(lines) and grad_neg_calc(lines) have been created.

Output: List with the x and y values for the pos and neg slopes.

### Step6: Restrict the min and max possible gradients/slopes
This helper function restrict_grad(grad, grad_max_thd, grad_min_thd) collected all x and y values for lines with a slope within the boundaries grad_max_thd and grad_min_thd.
Output: List with the x and y values for the restricted pos and neg slopes.

### Step7: Collecting all x1/x2 and y1/y2 for pos and neg restricted gradients/slopes
Just put all teh x1 and x2 values in 1 column and all the y1 and y2 values in another column with helper function all_val_one_lst(data). That is necessary for further processing.
Output: List with all x and y values in 2 column 

### Step8: Run the fittin line process
This part of the pipeline creates the data for the solid lines depending on the results out of Hough Transformation and further slope/gradient speration and restriction.
The helper function def fitting_line(x, y) computes with giben x and y values and the np.linalg.lstsq method a fitted line.
The function returns a slope and and a axis intercept

### Step9: Calculate the bottom and top x/y values of the fitted lines, adding boundaries
With the given slope and intercept out of the fittin_line function the bottom and and the top y7y values for positve and negative solid line can be caluclated.
Just for reall bad results rough boundaries are added.

### Step10: Draw the solid lines on the image
Now the solid lines are drawn on the original image
[image7]: ./test_images/solidsolidWhiteCurve.jpg 
![alt text][image7]


## 2. Identify potential shortcomings with your current pipeline

One shortcoming I experienced was following fact:
If after the seperation and restrictions of gradients no x/y values left fot the fitting line process. The function np.linalg.lstsq will end up in an error.
This is a problem when processing the video files, because getting an error it takes a lot of time to optimize the hough or gaussian parameters and starting creating the vido again.

For debugging reasons, it would be better to have a more robust algorithm to create the parameters for the solid lines.
Once optimized parameters are found for the hough and gaussion functions, it works fine. Took me a long time to figure that out.


## 3. Suggest possible improvements to your pipeline

A clear improvment would be a "pixel" independent code. I used the absolute values of pixelTo create the area of interest and for the x and y calculation of the solid line. To have realtive solution depending on image shape would be a better solution
I guess this is also teh reason, the callenge video does not work with my solution.



