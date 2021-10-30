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
4. Apply Canny detector on the masked images and obtain edges around the pupil.
5. Apply Hough transform to the edged image, which detects all possible circles in the image. Then loop through every circle and identify the one with the smallest distance to the approximated center found in step #3. The result is the pupil boundary.
6. Depending on different people, we notice that the iris radius is around 55-60 units larger than the pupil radius. We choose 55 + pupil_radius as the iris radius, assuming that both the pupil and the iris share the same center.
7. Draw the outer boundary and append each image's boundary and center information to desired variables.


## IrisNormalization


## IrisEnhancement


## FeatureExtraction

### Input
enhanced: the function inputs all the enhanced images from IrisEnhancement.

### Return
feature_vec: A numpy array with each element containing 1536 feature components aas defined in Li Ma's paper. 

### Functions
M(x,y,f): inputs x: x-coordinate, y: y-coordinate, and f: frequency and calculates the M1 modulating function mentioned in paper.

Gabor(x,y,dx,dy,f): inputs x,y, dx: space constant x, dy: space constant y, and f. It performs the gabor filterd defined in paper. 

block(dx,dy,f): inputs dx,dy, and f. Implements gabor filtering on an 8 x 8 region with predetermined parameters dx,dy, and f.

get_vector(vector1,vector2): inputs two filtered images and computes the mean and standard deviation of each 8 x 8 block. Finally it returns a featured vector with means and stds of two different channels appended in the specified order as mentioned in Li Ma's paper.

### Logic
1. Define two channels using specified space constants as mentioned in Li Ma's paper.
2. Obtain the ROI by slicing the normalized image to 48 x 512, as defined in paper.
3. Implement the convolution method on two channels and obtain two filtered images.
4. Run get_vector() function using the two filtered images from step #3
5. Obtain the desired feature vector. 







