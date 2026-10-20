2026-10-20 09:10

Status:

Tags: [[Computer Vision]]


# Finding Shapes


LECTURE 1

|
|
|
|
|

#### Hough Transform for Circles
- It is duality:
	- $(x − x_0)^2 + (y − y_0)^2 = r^2$ 
- Points: $x, y$ centre $x_0, y_0$ radius: $r$
	![[Pasted image 20261020092127.png]]

#### Circle Voting and Accumulator Space
- Left side (image space): Edge pixels lie on circles to be detected
- Right side (parameter space): Each edge pixel votes for possible circle parameters , forming cone-like surfaces.
	![[Pasted image 20261020092403.png]]
- Accumulator: Stores the number of votes for each parameter combination.
- Detection: Peaks occur where votes overlap, indicating likely circles.
- Pseudocode:
	![[Pasted image 20261020092516.png]]
- Result:
	![[Pasted image 20261020092612.png]]

#### Extensions to conic sections
- Ellipse:
	![[Pasted image 20261020092658.png]]
	- described by 4 parameters (i.e. $x_0, y_0, a, b$)
- If each has 100 values, accumulator size:
	- $10^2 ×10^2 ×10^2 ×10^2 = 10^8 = 0.1$GB
- Add rotation, that is $10$GB
- Motivates approaches to save memory and improve speed (since result is optimal)

#### Speeding it up
- Use the circular shape as an example
- Its a 3D accumulator
	![[Pasted image 20261020093103.png]]

#### Fireside 
![[Pasted image 20261020093902.png]]

#### Arbitrary Shapes 
- Used Generalised Hough transform
- Form (discrete) look-up-table (R-table)
- Vote via look-up-table

#### R-table Construction
- 