# MeanshiftTracking
Meanshift is a popular mode seeking algorithm which is previously used for image segmentation and object tracking. It offers an efficient iterative procedure to find the maximum of a convex function. At each iteration, the current estimated mean of the density is shifted towards the highest density location, and it finally converges at the maximum density point of the surface.
The “Kernel-based object tracking” paper of Comaniciu et al. describes the application of the meanshift theory to object tracking. There are also very good tutorials such as this one and this one, that you can access freely on internet. So I will not try to give any details about the theory, instead will just tell some key points about the implementation.
I have implemented the original version of the algorithm using OpenCV (version 2.4.8) and MS Visual C++ 2012 Professional Edition on MS Windows 7.

Since the original algorithm itself is a color-based tracker using color histograms, using 1D intensity histogram did not give satisfactory results. So I discarded the Blue channel to reduce the computational burden, and used 2D weighted color histogram of Red and Green values. Weighting the histogram with a Gaussian kernel (Comaniciu et al. uses Epanechnikov kernel) gave good results. While weighting, you just build a 2D Gaussian kernel with the same size of the target region, and use the corresponding weight value to increment the bin of the corresponding pixel in that location. Finally, you should normalize the histogram by dividing each bin to the sum of the histogram, which yields a histogram that sums up to 1.
I have also implemented the “background-weighted histogram” extension, described in section 6.1. The weighting provides suppression of histogram bins (colors) of the target candidate, which is also dominant in the background. I have named the updated version as meanshiftBG.

The implementation I share here is not scale adaptive, so I will try to give a scale adaptive version later.
You can check this and this website for popular test sequences published in the literature.

# Usage
You can pass a video file full path as command argument, or a live webcam stream with “–withCamera” option. Check main.cpp.
You can pause the video any time by pressing “p”, and draw a rectangle region of interest by pressing the left mouse button and dragging until the region of interest is covered.
"# Meanshift-Tracking" 
