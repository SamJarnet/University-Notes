2026-10-09 11:10

Status:

Tags: [[Computer Vision]]


# Point Operators

#### An image and its Histogram
- Plots number of pixels with a particular brightness level
- The histogram shows contrast (the range of brightness levels
	![[Pasted image 20261009111211.png]]

#### Different Histograms
- Example: Histogram of 10,000 points in $[-4, 4]$
- Ordinary Histogram
	![[Pasted image 20261009111447.png]]
	- The number of pixels with a particular value
- Cumulative Histogram
	![[Pasted image 20261009111511.png]]
	- The number of pixels $\leq$ a particular value
	- Can also be scaled so that the highest frequency is 1 by dividing the total number of pixels/points

#### Modifying Image Intensity
- You can do this by choosing values for $k$ and $l$ 
	![[Pasted image 20261009111731.png]]

#### Intensity mappings
![[Pasted image 20261009112029.png]]


#### Applying Exponential and Logarithmic Point Operators
- Brightness compression:
	![[Pasted image 20261009112216.png]]
		![[Pasted image 20261009112222.png]]
	- Logarithmic compression
- Brightness expansion
	![[Pasted image 20261009112247.png]]
		![[Pasted image 20261009112319.png]]
	- Exponential expansion

#### Intensity Normalisation
- Toy example
	![[Pasted image 20261009112400.png]]
- The aim is to use all available grey levels for display
	![[Pasted image 20261009112611.png]]
	
	![[Pasted image 20261009112631.png]]

#### Histogram Equalisation
- Toy example:
	![[Pasted image 20261009112721.png]]
- The aim is a flat histogram
	![[Pasted image 20261009112901.png]]

#### Intensity Normalisation and Histogram Equalisation
- Grey levels all "weigh" the same
	![[Pasted image 20261009113020.png]]
- Grey levels have different weights
	- Aimed for human vision

#### Thresholding 
- Thresholding selects points that exceed a chosen threshold $\tau$ 
	![[Pasted image 20261009113645.png]]
	- $x,y$ are coordinates
	
	![[Pasted image 20261009113709.png]]

- Manual Vs Automatic Thresholding:
	![[Pasted image 20261009114032.png]]

#### Otsu Thresholding
- Percent of the number of pixels in each group (separated by $\tau$) against the total number of pixels
	![[Pasted image 20261009114137.png]]

	![[Pasted image 20261009114152.png]]

	![[Pasted image 20261009114257.png]]

#### Adaptive Thresholding
- Starting with initialised $\tau^{(0)}$, e.g. the mean of given image find a proper threshold iteratively by 
	![[Pasted image 20261009114442.png]]

	![[Pasted image 20261009114449.png]]