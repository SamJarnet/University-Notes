2026-11-06 13:01

Status:

Tags: [[Computer Vision]]


# Types of Image Feature and Segmentation

#### Types of features
- Global features:
	- A Global feature is extracted from the contents of the entire image
		![[Pasted image 20261106130317.png]]
- Grid or Block-Based Features
	- Multiple features are extracted; one per block
		![[Pasted image 20261106130612.png]]
- Region-based Features
	- Multiple features are extracted; one per region
		![[Pasted image 20261106131307.png]]
- Local Features
	- Multiple features are extracted; one per local interest point
		![[Pasted image 20261106131335.png]]

#### Image Histograms
- In second lecture we saw global feature computed from the average of the colour bands
	- This wasn't robust and couldnt deal ell with multiple colours in the image
- A more common approach to computing a global image description is to compute a histogram of the pixel values.

#### Joint-Colour Histograms 
- A joint colour histogram measures the number of times each colour appears in an image.
	- 3 channel histogram: R 256 + G 256 + B 256 vs
	- joint histogram: R 256 x G 256 x B 256
- The colour space is quantised into bins, and we acumulate the number of pixels in each bin
	- Technically it's a multidimensional histrogram, but we flatten it (unwrap) to make it a feature vector
	![[Pasted image 20261106131734.png]]
- Normalisation (i.e. by the number of pixels) allows the histogram to be invariant to image size.
- Choice of colour-space can make it invariant to uniform lighting changes (e.g. H-S histogram)
- Invariant to rotation
- But vastly different images can have the same histrogram

#### Image Segmentation 
- The first part of the process is creating region-based descriptions
	- The process of partitioning the image into sets of pixels and often called segments
	- Pixels within a segment typically share certain visual characteristics.

#### Global Binary Thresholding
- Thresholding is the simples form of segmentation
	- Turns grey level images into binary images (i.e. two segments) by assigning all pixels with a value less than predetermined threshold to one segment, and all other pixels to the other
	- Really fast
	- Requires a manually set static threshold
		- Not robust to lighting changes
		- Can work well in applications with lots of physical constraints (lighting control and/or high-contrast objects)

#### Otsu's Thresholding Method
- Provides a way to automatically find the threshold.
	- Assume there are two classes (i.e. foreground and background)
	- The histrograms must have two peaks
- Exhaustively search for the threshold that maximises interclass variance
	![[Pasted image 20261106144727.png]]

#### Adaptive / local thresholding 
- Local (or adaptive) thresholding operators compute a different threshold value for every pixel in an image based on the surrounding pixels
	- Usually a square or rectangular window around the current pixel is used to define the neighbours
- Mean adaptive thresholding:
	- Set the current pixel to 0 if its value is less than the mean of its neighbours plus a constant value; otherwise set to 1
	- Parameters:
		- size of window
		- constant offset value
	![[Pasted image 20261106145027.png]]
- Good invariance to uneven lighting/contrast
- But:
	- Computationally expensive (at least compared to global methods)
	- Can be difficult to choose a window size
		- If the object being imaged can appear at different distances to the camera then it could break
	![[Pasted image 20261106145226.png]]

#### Segmentation with K-Means 
- K-Means clustering also provides a simple method for performing segmentation:
	- Cluster the colour vecotrs (i.e. [r, g, b]) of all the pixels, and then assign each pixel to a segment based on the closest cluster centroid.
	- Works best if the colour space and distance function are compatible 
		- e.g. Lab colour-space is desiged so that Euclidean distances are proportional to perceptual colour differences
	![[Pasted image 20261106150215.png]]
- Naive approach to segmentation using k-means doesn't attempt to preserve continuity of segments
	- Might end up with single pixels assigned to a segment, far away from other pixels in that segment
- Can also encode spatial position in the vectors being clustered: [r, g , b, x , y]
	- Normalise x and y by the width and height of the image to take away effect of different images sizes
	- Scale x and y so they have more or less effect than the colour components
	![[Pasted image 20261106150456.png]]

#### Advanced Segmentation Techniques 
- Lots of ongoing reserach
	- Techniques that can automatically determine the number of segments
	- "semantic segmentation" techniques that try to create segments that fit the objects in the scene based on training examples

#### Pixel Connectivity
- A pixel is said to be connected with another if they spatially adjacent to each other
	- Two standard ways of defiing this adjacency:
		- 4-connectivity
		- 8-connectivity
	![[Pasted image 20261106150717.png]]

#### Connected Component 
- A connected component is a set of pixels in which every pixel is connected either directly or through any connected path of pixels from the set
	![[Pasted image 20261106150818.png]]
- Connected Component Labelling is the process of finding all the connected components within a binary (segmented) image
	- Each connected segment is identified as a connected component
- Lots of different algorithms to perform connected component labelling
	- Different performance tradeoffs (memory versus time)

#### Two-Pass algorithm (Union-Find)
- 1. First pass:
	- a. Iterate through each element of the data by Raster Scanning
		- i. If the element is not the background
			- 1. Get the neighbouring elements of the current element
			- 2. If there are no neighbours, uniquely label the current element and continue
			- 3. Otherwise, find the neighbour with the smallest label and assign it to the current element.
			- 4. Store the equivalence between neighbouring labels
- 2. Second pass:
	- a. Iterate through each element of the data by Raster Scanning
		- i. If the element is not in the background
			- 1. relabel the element with the lowest equivalent label
	![[Pasted image 20261106151453.png]]
	![[Pasted image 20261106151504.png]]