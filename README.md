# T-Shirt-Detection
This project is a solution to the problem of having to track a single person in a crowd of people. The problem with detecting a particular person in a frame is that every person has different features we can use to identify them, but teaching these features to a model becomes a difficult task, especially if there are more than one person using the code. Deep learning models trained to detect people go a long way to solving this problem, but cannot effectively detect only a particular person in the image unless the model  is trained only on that  particular person. 
The method I have come up with to solve this problem is to differentiate between people based on the colour of their t-shirt. The code uses a simple colour thresholding algorithm in the HSV colour space to detect the t-shirt, coupled with algorithms to recaliberate the t-shirt colour, and eliminate backgrounds and nearby people. 
There are multiple ways to control this program:
a) Manually clicking on the person to be tracked
b) Person to be followed stands in front of the camera and says "follow me". 

ALGORITHM:
1) When the person to be detected stands in front of the camera and says follow me; the algorithm takes a small region around the centre of the frame and calculates its average colour.

2) This average colour is used to calculate the initial position of the tshirt. We threshold the image in a region of +-30 of the average colour, and find an initial contour representing the tshirt. 

3) We calculate the center of this contour and use this as the reference point for the remaining detection. 

4) The value of a particular colour changes with the lighting conditions, and also as the person moves away or towards the camera. To solve this issue, we constantly recaliberate this colour by assuming a small region around the initial center. The code recalculates the average colour around the center of the contour and updates this average every 0.5 seconds. This average is again used to recalculate the new center of the tshirt.

5) Another problem that arises is that if the background is a similar colour to the t-shirt, or another person in the frame is wearing a similar t-shirt. This problem is solved again using a bigger region around the initial center. We assume a bigger region around the initial center, because the person to be detected has to be around a region of his tshirt. We simply create a mask of the frame keeping only the part of the image in this region and removing every other part of the frame. This region is also constantly updated as the person moves, due to change in the centre point of the t-shirt. This ensure that anyone else wearing the same t-shirt colour does not affect the tracking process, as they arent in the intial region around the center.

Note: The program can be made more accurate by adding extra image filtering techniques. The values used in the program can be tweaked for better performance. Also the colour spaces can also be changed according to the need. The value of calculated centre can also be smoothed.   
