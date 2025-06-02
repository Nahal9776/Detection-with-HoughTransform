# Road Lines and Street Signs Detection with the Hough Transform
# Objectives
Detect the street lines and the circular road signs:
• Find the edges (e.g., with Canny)
• Find the street lines with the Hough Transform, first using OpenCV and then manually
• Implementing the Hough Transform
• Find the circles corresponding to road signs (in this case only OpenCV implementation)

# Implementation
# 2.1 Import the necessary libraries
I began by installing the most recent version of OpenCV using pip.
# 2.2 Road lines Detection
I have a variable called image path, which contains the file path to an image file provided by the exercise. This image is loaded using the OpenCV library with the cv.imread() function. The loaded image is stored in a variable called image. To display the image, I’m using a function show img function that was provided.

# 2.3 Edge extraction using the Canny algorithm
I have first started by some preprocessing steps (Grayscale Conversion and Blurring) which I found really usefull in helping to find the best parametrs for canny edge detection. I’ve created a window using OpenCV with two trackbars for adjusting the threshold values of the Canny edge detection algorithm. The trackbars are labeled ”Threshold1” and ”Threshold2”. I’m using a simple callback function, nothing(x), for the trackbars. Inside a loop, I continuously read the current threshold values from the trackbars which I have tried to optimize manually. I then apply the Canny edge detection algorithm to the image and interactively changed the values of the threshold to find the best parametrs while displaing both the original image and the edges in separate windows. The loop continues until I press the ’q’ key. After exiting the loop, I print the best threshold values based on the last positions of the trackbars. At the end I have visualized the result of the Canny algorithm with the best thresholds values (0,701) in the next cell.

# 2.4 Hough transform to detect lines
In this code, I’ve created the same graphical interface like the last section using OpenCV that allows me to fine-tune the parameters of the Hough transform for detecting lines in an image. I previously applied Canny edge detection to the image to enhance the edges, and now, using trackbars, I can dynamically adjust the Hough transform parameters such as Rho, Theta, and Threshold. The transformed image with detected lines is then displayed in real-time, allowing me to visually assess the impact of parameter changes on the line detection. In next cell, I’ve visualized the results of the Hough transform with the previously identified best parameters. First, I applied Canny edge detection to the blurred image using the optimal thresholds. Then, I employed the best parameters for the Hough line detection, for line detection (hough threshold). The detected lines were drawn on the original image, and two additional visualizations were created: one showing the Canny edges and another display ing the original image with the detected lines filled in red.

# 2.5 Custom implementation of the Hough
# Transform
In this custom defined python function, hough lines new, I implemented the Hough transform to detect lines in an edge image. The function takes in the edge image, a threshold for line detection, and the minimum and maximum angles for line searching. Internally, it initializes a polar coordinate accumulator matrix, iterates over edge points, updates the accumulator based on calculated rho values, and identifies lines with accumulator values surpassing the specified threshold. The function then converts these detected lines from polar to
Cartesian coordinates before returning them. The function begins by initializing a polar coordinate accumulator matrix, considering the entire range of possible angles and distances (rho values). It then iterates through the edge points of the input image, updating the accumulator based on the calculated rho values for different angles. This process essentially
creates a voting system where the most prominent lines accumulate higher counts in the matrix. The lines are then extracted by identifying the peaks in the accumulator matrix that exceed the specified threshold. The result is a set of lines represented in both rho and theta (polar) coordinates. In the next cell we will call the above function to find lines using the implemented Hough transform and then will draw the lines and fill the area between them using the given functions and we will show the changed images.

# 2.6 Road signs detection using the Hough
# Transform
In this code, initially, I converted the input image to grayscale and then to uint8 format to ensure compatibility with the Hough transform algorithm . I’ve created the same graphical interface like the last sections using OpenCV that allows me to fine-tune the parameters of the Hough Circles for detecting road signs in an image. I have interactively optimized the parameters through the trackbars until the desired circle detection outcome is achieved. The script runs in a loop, displaying the modified image with detected circles in a separate window. The execution can be interrupted by pressing the ’q’ key, closing the windows and concluding the interactive parameter tuning process. in the next cell, I have visualizde the result of the Hough transform using the parameters that were manually tuned to achieve the best circle detection outcome. I set the parameters (param1 = 700 ,param2 = 10 ,min radius = 8 max radius = 10) to specific values that were found through the interactive parameter tuning process. The HoughCircles function is then applied to the uint8 grayscale image with the chosen parameters.
