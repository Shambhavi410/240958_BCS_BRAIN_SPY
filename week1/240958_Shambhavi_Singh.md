Edge Detection using Convolution Kernels

I first converted the image to grayscale.
Then I used Gaussian Blur (3x3) kernel to remove noise from the image to avoid extra unwanted edges. 
gaussian_kernel = (1/16) * np.array([
    [1, 2, 1],
    [2, 4, 2],
    [1, 2, 1]
])
Tried using different kernels of gaussian blur to improve edges.
I tried sharpening it using another kernel (and trying different kernels) after this. It detected more edges but the edges became noisy.


