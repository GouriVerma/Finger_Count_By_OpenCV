## Overview
The project includes the implementation of OpenCV to count the number of fingers being shown on screen. 

## Step 1: Calculating static background
A part of the screen is chosen and accumulated weight is calculated for that part. This helps to get the static background which is used further for difference when hand comes inside the frame. This process is done by finding accumulated weight for initial 60 frames. Accumulated weight is found for all of the gray frames.

## Step 2: Segmenting the hand
ROI is retrieved from the whole frame captured, then absdiff is found between background and the new frame's ROI which helps to get only the new things which came into the frame. After getting the difference, it is thresholded to get only hand portion as white and rest as black. This threshold is passed to findContour function which helps to get the external contour of hand. The contour with largest area is considered to be the contour of hand. 

## Step 3: Counting the number of fingers:
The topmost, bottommost, leftmost and rightmost points are derived from the contour and maximum of all those is found. The centre of hand is calculated by ((left+right)//2) and ((top+bottom)//2). A completely black image of same dimesnions as threshold is made and a white circle of certain width say 20 is drawn from the centre of radius 0.6*max distance on that black frame. The bitwise and is found for this new frame with circle and the thresholded to only get the portions of threshold lying in the width of circle. This final part involves discrete portions of fingers and wrist. Ignoring the contour of wrist, the number of contours is counted and the number of contours represent the number of fingers.
