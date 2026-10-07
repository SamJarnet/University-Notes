2026-10-02 15:56

Status:

Tags: [[Computer Vision]]


# Image Formation

#### Decomposing an Image into its Bits
- The most Significant Bit carries the most information whereas bit 0 is noise.
	![[Pasted image 20261002155727.png]]
	![[Pasted image 20261002155848.png]]
- Here, bit 4 is the lighting
- Effects of differing image resolution:
	![[Pasted image 20261002155918.png]]
- Low resolution lose information but N by N points implies large storage use. How do we choose an appropriate value for N?

#### What are waves?
- 2D waves are along x and y axes simulateneously
- $𝑒^{𝑗𝜔𝑡} = cos (𝜔𝑡) + 𝑗 sin (𝜔t)$
- 𝑗: the complex number 𝑗 = $\sqrt{−1}$ 
- Frequency:
	![[Pasted image 20261002161919.png]]

#### Fourier
- Any periodic function is the result of adding up sine and cosine waves of different frequencies
	![[Pasted image 20261002162002.png]]
- Inverse forier:
	![[Pasted image 20261002162216.png]]
- Fourier Transform in Action:
	![[Pasted image 20261002162514.png]]
- Other forms of fourier:
	![[Pasted image 20261002162622.png]]

#### Example:
- A rectangular pulse and its Fourier Transform
	![[Pasted image 20261002162709.png]]
- Pulse:
	![[Pasted image 20261002162725.png]]
- Use fourier:
	![[Pasted image 20261002162738.png]]
- Evaluate Integral:
	![[Pasted image 20261002162804.png]]
- Get result:
	![[Pasted image 20261002162820.png]]

#### Reconstructing a signal from its Fourier Transform
- Using the sum of the inverse fourier transform:
	![[Pasted image 20261002163018.png]]
- Gets you the reconstruction
	![[Pasted image 20261002163011.png]]

#### Magnitude and Phase of Fouirer Transform of a Pulse
![[Pasted image 20261002163203.png]]