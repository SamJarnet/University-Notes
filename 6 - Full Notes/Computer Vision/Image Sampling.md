2026-10-06 09:07

Status:

Tags: 


# Image Sampling

#### 1D Discrete Fourier Transform
- Continuous Fourier:
	![[Pasted image 20261006091129.png]]
- Discrete Fourier calculates frequency from data points
	![[Pasted image 20261006091156.png]]
- Continuous Inverse Fourier:
	![[Pasted image 20261006091236.png]]
- The Discrete Inverse Fourier:
	![[Pasted image 20261006091220.png]]

#### Tranform Pair for Sampled Pulse
- ![[Pasted image 20261006091421.png]]
- Signal Reconstruction from its transform components
	![[Pasted image 20261006091451.png]]

#### 2D Fourier Transform
- Two Dimensions of space, x and y
- Two Dimensions of frequency, u and v
- Forward transform:
	![[Pasted image 20261006091847.png]]
- Inverse Transform:
	![[Pasted image 20261006091908.png]]

#### Reconstruction
![[Pasted image 20261006091934.png]]

#### Shift Invariance
- Shift
	![[Pasted image 20261006092820.png]]
- Rotation
	![[Pasted image 20261006092848.png]]
- Filtering
	![[Pasted image 20261006092908.png]]

#### Applications of 2D FT
- Understanding and analysis 
- Speeding up algorithms
- Representation (invarience)
- Coding
- Recognation/understanding (e.g. texture)

#### Sampling Signals
- Original continuous signal
	![[Pasted image 20261006093218.png]]
- Good sampling
	![[Pasted image 20261006093237.png]]
- Bad sampling (aliased) 
	![[Pasted image 20261006093256.png]]

#### Sampling Function
![[Pasted image 20261006093522.png]]


- Fourier Transform Property:
	![[Pasted image 20261006093930.png]]
	- Convolution
	![[Pasted image 20261006093904.png]]

#### In the Frequency Domain
- Spectra Retreat
	![[Pasted image 20261006094107.png]]
- If sampling is just right, spectra just touch
	![[Pasted image 20261006094118.png]]
- Minimum sampling frequency = 2 * max
	![[Pasted image 20261006094133.png]]

#### Sampling Theory
- Nyquist's Sampling theorem:
	- In order to be able to reconstruct a signal from its sample we must sample at minimum at twice the maximum frequency in the original signal
- E.g. speech 6kHz, sample at 12 kHz
- Video bandwidth (CCIR) in 5Mhz
- Sampling at 10Mhz gae 576x576 images
- Guideline: "two pixels for every pixel of interest"
- Alias:
	![[Pasted image 20261006094524.png]]
