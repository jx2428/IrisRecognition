# IrisRecognition

## IrisLocalization
The function IrisLocalization(images) preprocesses all the input images and apply Hough transform to detect the pupil circle(inner boundary) and the iris circle(outer boundary) of each image.

### Input
images: A list of train/test images from the CASIA image database.

### Return
boundary: A list of all images with the outer boundary drawn.
center: A list of all pupil centers of each image. Each pupil center is an element of length 3 of the list center. Each element of the list contains x-coordinate, y-coordinate, and the radius of the pupil center. 

### Logic 
1. Apply bilateral filter to blur each image with the purpose to reduce noise.
2. Project each image both horizontally and vertically and find the local minimum, which is notated by (X_p,Y_p) in the function. This is the aproximated pupil center because the local minimum is the darkest region.
3. Create a 120 x 120 region around (X_p,Y_p) as mentioned in Ma's paper; and then recalculate the pupil center using same procedures mentioned in step #2.
