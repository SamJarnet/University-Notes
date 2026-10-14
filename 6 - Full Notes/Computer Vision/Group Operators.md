2026-10-09 12:55

Status:

Tags: [[Computer Vision]]


# Group Operators

#### 3x3 template and its inverse
-  A template is also called a kernel or a filter
	-  it is a small grid of weights that you move across an image to process it
- Flip corresponding to both directions
	![[Pasted image 20261009125653.png]]

#### Template Convolution
- Convolution is the process of moving the template across the image and calculating a new pixel value at each position
- Template is actually flipped around both axes
- This does not matter for symmetric templates
	![[Pasted image 20261009125801.png]]
- In a continuous domain:
	![[Pasted image 20261009125817.png]]

- Calculate a new image from the original
- Template is inverted for convolution 
- Template is convolved in a raster fashion (across each row, then down to the next row)
	![[Pasted image 20261009130017.png]]



