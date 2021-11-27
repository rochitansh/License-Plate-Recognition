# Object Detection using CPP
CPP code for Edge Detection(License Plate Recognition) using OPENCV
## What is OPENCV ?
OpenCV (Open Source Computer Vision Library) is an open source computer vision and machine learning software library. OpenCV was built to provide a common infrastructure for computer vision applications and to accelerate the use of machine perception in the commercial products.

OpenCV is a cross-platform library using which we can develop real-time computer vision applications. It mainly focuses on image processing, video capture and analysis including features like _face detection_ and _object detection_

## Detecting Edges using OPENCV in C++
Edge detection is an image-processing technique, which is used to identify the boundaries (edges) of objects, or regions within an image. Edges are among the most important features associated with images. We come to know of the underlying structure of an image through its edges. Computer vision processing pipelines therefore extensively use edge detection in applications.
#### How are Edges detected? 
Edges are characterized by sudden changes in pixel intensity. To detect edges, we need to go looking for such changes in the neighboring pixels

There are two techniques available for edge detection
- Sobel Edge detection
- Canny Edge detection

#### Preliminary Step:
The first step is to import the opencv library. Then we will read the image, using the imread() function in OpenCV. The image will be Colored image but we convert it into grayscale image because in grayscale images, Pixels are more easily detectable and the information of each pixel is obtained easily.

The Next step is to Blur the image using _GaussianBlur()_ function.This is done  to reduce the noise in the image. In edge detection, numerical derivatives of the pixel intensities have to be computed, and this typically results in ‘noisy’ edges.Blurring smoothens the intensity variation near the edges, making it easier to identify the predominant edge structure within the image. 

Degree of Blurring is provided by the size of the Convolution kernel( in our case, 3 x 3)

Syntax: **GaussianBlur(img, img_blur, size(3 x 3), SigmaX=0, SigmaY=0);**

## Sobel Edge Detection
The Sobel Operator detects edges that are marked by sudden changes in pixel intensity.we can approximate the derivative, using a 3×3 kernel. We use one kernel to detect sudden changes in pixel intensity in the X direction, and another in the Y direction.

 Let G_x and G_y represent the intensity gradient in the x and y directions respectively. If A and B denote the X and Y kernels:
 
 <img src="https://latex.codecogs.com/png.latex?G_x=A*I" title="G_x=A*I" />
 
 <img src="https://latex.codecogs.com/png.latex?G_y=B*I" title="G_y=B*I" />
 
 where * denotes the covolution operator, and _**I**_ represents the input image.
 The final approximation of the gradient magnitude, G can be computed as 
 
<img src="https://latex.codecogs.com/png.latex?G=\sqrt{G_1&space;*&space;G_2}" title="G=\sqrt{G_1 * G_2}" />

Syntax: **Sobel(src, ddepth, dx, dy)**

The parameter **ddepth** specifies the precision of the output image, while **dx** and **dy** specify the order of the derivative in each direction. For example:

 If **dx=1** and **dy=0**, we compute the 1st derivative Sobel image in the x-direction.
 
 ## Canny Edge Detection
 
 The algorithm itself follows a three-stage process for extracting edges from an image. Add to it image blurring, a necessary preprocessing step to reduce noise. This makes it a four-stage process, which includes:
 1) Noise Reduction
 2) Calculating Intensity gradient of the image
 
 The above two steps are as same as Sobels method 
 
 3) Suppression of false Edges:

After reducing noise and calculating the intensity gradient, the algorithm in this step uses a technique called non-maximum suppression of edges to filter out unwanted pixels (which may not actually constitute an edge). To accomplish this, each pixel is compared to its neighboring pixels, in the positive and negative gradient direction. If the gradient magnitude of the current pixel is greater than its neighbouring pixels, it is left unchanged. Otherwise, the magnitude of the current pixel is set to zero.

 4) Hysteresis Thresholding:

In this final step of Canny Edge Detection, the gradient magnitudes are compared with two threshold values, one smaller than the other.
- If the gradient magnitude value is higher than the larger threshold value, those pixels are associated with strong edges, and are included in the final edge map.
- If the gradient magnitude values are lower than the smaller threshold value, the pixels are suppressed, and excluded from the final edge map.
- All the other pixels, whose gradient magnitudes fall in between these two thresholds, are marked as ‘weak’ edges (i.e. they become candidates for being included in the final edge map).
- If the ‘weak’ pixels are connected  to those associated with strong edges, then they too are included in the final edge map. 

syntax: **Canny(image, threshold1, threshold2)**

 
 


