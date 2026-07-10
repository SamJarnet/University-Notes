23-12-2024 18:45

Status:

Tags: [[Computer Systems I]]


# GPU

#### What is a GPU?
- Graphics Processing Unit
- Made for gaming

#### Why do we need GPUs?
- Graphics is maths intensive
	- 1920x1080 = 2 Mega Pixels…   6.2 MB
	- 2560x1440 ≈ 3.7 Mega Pixels…  11 MB
	- 3840x2160 ≈ 8.3 Mega Pixels…  24.9 MB
- 3D drawing, rendering and shading needs lots of per-pixel maths
- [[CPU]]s are not very efficient at this


#### Representing Objects:
- We represent 3D objects as a polygon mesh of:
	- Vertices, Edges, Faces
	- 
#### Typical Transformation maths:
![[Pasted image 20241228150325.png]]
- This is a perspective transformation (so objects vanish into the distance)
- Note this turns into a lot of multiply add sin/cos maths for each set of coordinates


#### GPU capability over time:
- Early GPUs used fixed-function pipelines
- Early 2000s saw the introduction of programmable shading
	- Almost as flexible as CPUs for looping floating-point maths, but orders of magnitudes faster
- Now "generic" stream processing units allow GPUs to be more general computing devices


#### GPUs are now used for:
- Video compression
- Video transcoding
- Image processing
- Modelling
- Autonomous vehicles
- Machine learning/AI
- Number-crunching
- Crypto mining


#### CUDA cores:
- A "streaming multiprocessor" includes 128 CUDA "cores
- A CUDA core contains a floating point unit and sometimes an integer unit
	- Parallelising certain types of instructions
- Special Function Units are trigonometric operations
- RTX 4090 has 128 Streaming Multiprocessors 

#### D[[RAM]] bandwidth:
- Needs to be huge - so DRAM chips are arranged around the GPU

#### Tensor Cores:
- Cores targeted for AI acceleration
- Specifically for fused multiply-add (FMA) operations
	- Extensively used in neural networks
	- Used for Nvidia's DLSS technology

#### Summary:
- GPUs were originally just graphics co-processors
- Now do much more than graphics
	- GOGPU, AI, number crunching, rendering...
- Different architecture to CPUs
	- More of a vector-processing role







# References