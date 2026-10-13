2026-10-13 14:04

Status:

Tags: 


# Edge Detection

#### What is an edge?
- Its contrast:
	![[Pasted image 20261013140449.png]]

#### First Order Edge Detection
- Vertical edges, Ex 
	![[Pasted image 20261013141650.png]]
- Horizontal edges, Ey
	![[Pasted image 20261013141709.png]]
- Vertical and horizontal edges
	![[Pasted image 20261013141736.png]]
	
	![[Pasted image 20261013141745.png]]

#### Horizontal Differencing
- Horizontal differencing detects vertical edges
	![[Pasted image 20261013141842.png]]

	![[Pasted image 20261013143928.png]]

#### Vertical Differencing
- Vertical differencing detects horizontal edges
	![[Pasted image 20261013143956.png]]

	![[Pasted image 20261013144003.png]]

#### First Order Edge Detection
- Addition of horizontal and vertical
	![[Pasted image 20261013144027.png]]
	
	![[Pasted image 20261013144032.png]]

- Template:
	![[Pasted image 20261013144055.png]]
- Code:
	![[Pasted image 20261013144106.png]]

#### Taylor Series - evaluate $f(t + \Delta t)$ 
- To approximate a function $f$ 
	![[Pasted image 20261013144234.png]]

#### Edge Detection Maths
- Taylor expansion for $f(x + \Delta x)$ and $f(x - \Delta x)$ 
	![[Pasted image 20261013144341.png]]
- $(A)$:
	![[Pasted image 20261013144454.png]]
- $(A) - (B)$ :
	![[Pasted image 20261013144512.png]]
- Template for first order difference:
	![[Pasted image 20261013144556.png]]

#### Edge Detection in Vector Format
- Vectors have magnitude (strength) and direction
- Magnitude: $M=\sqrt{M_x^2 + M_y^2}$
- Direction: $\theta = \tan^{-1}(\frac{M_y}{M_x})$ 
	![[Pasted image 20261013144743.png]]

#### Templates for 3x3 Prewitt Operator
- Average Improved Horizontal and Vertical operators
	![[Pasted image 20261013145101.png]]
- Edge magnitude and direction calculated for centre point 
- Applying the Prewitt Operator
	![[Pasted image 20261013145228.png]]
	- No missing points
	- Blurred edges
	- No double points
	- So  use vectors 
	- displaying directions as an image communicates nothing

#### Templates for Sobel Operator
- Sobel is the most popular basic operator
- Double the centre coefficients of Prewitt
	![[Pasted image 20261013145614.png]]

#### Generalising Sobel - use Pascal's triangle
- 1. Averaging:
	![[Pasted image 20261013145720.png]]
- 2. Differencing
	![[Pasted image 20261013145732.png]]

- Generalised Sobel:
	- Generalised by: averaging$^T$ * (differencing):
		![[Pasted image 20261013145910.png]]
	- s =Sobel_templates (5)
	- s(:, :, 1) = 
		![[Pasted image 20261013145945.png]]
