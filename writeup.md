#Project 1 - Finding Lane Lines

##Project Goals
1. Create a lane finding pipeline over a series of images, then apply the result to a video stream, annotating left and right lanes with solid lines.

2. Reflect on the project describing potential shortcomings and suggest possible improvements.

##Reflection

### Pipeline
To discover lane lines the following pipeline was employed.
1. Read images from disk then created a copy.
2. Converted the copied image to grayscale.
3. Applied a Gaussian blur filter.
4. Applied a region mask to a portion of the blurred, grayscale image where it can be reasonably expected to detected lane lines.
5. Applied Canny edge detection to the masked image region.
6. Applied Hough Line detection to Canny image.
7. Overlaid lane lines on top of detected lines by modifying the `draw_lines()` function using the following procedure.
  - Calculated the gradient of each detected line, categorizing lines based on positive or negative slope, where positively sloped lines represent the left lane, and negatively sloped lines represent the right line. Some detected lines were of infinite slope and were ignored.
  - Averaged the `x` and `y` positions for the right lane and the left lane individually, along with their gradients, and used the values to extrapolate the entirety of the lane line from the bottom of the image to the furthest extent of the detected lane lines.
8. Overlaid the extrapolated lines on top of the original image.
9. Applied the line detection method to the videos. `solidWhiteRight.mp4` and `solidYellowLeft.mp4`.

### Shortcomings
- A major shortcoming of this method of lane detection is it does not perform well on sharp turns.

### Improvements
- A better method of lane detection would account for sharper curves, and have a more accurate method of accounting for gaps in lane lines.
