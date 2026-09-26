2026-09-23 20:51

Status:

Tags: [[Foundation of Machine Learning]]


# Introduction

#### What is Machine Learning?
- The field of study that gives computers the ability to learn without being explicitly programmed
	![[Pasted image 20260923205530.png]]
- A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks is T, as measured by P, improves with experience E.

#### Traditional Programming vs Machine Learning
- Traditional:
	- Data + Rules -> Answers. You write explicit rules
- Machine Learning:
	- Data + Answers -> Rules. The machine learns the rules or patterns from data, i.e. data fitting.

#### The Three Main Paradigms of ML
- Supervised Learning:
	- Learns from labelled data. Goal: Predict a label for new, unseen data. Examples:
		- Face Recognition
		- House price prediction
- Un(or self) supervised Learning
	- Finds patterns in unlabelled data. Goal: Discover hidden structure or groupings. Examples:
		- Topic modeling
		- Pretraining in ChatGPT
- Reinforcment Learning
	- Learns through trial and error in an environment. Goal: Maximise a cumulative reward signal. Examples:
		- Game playing
		- Robotics

#### ML Workflow: A step-by-step process
- Problem Definition: What question are we trying to answer?
- Data collection & Preparation: Gather, clean, and format data. This is often 80% of the work.
- Preprocessing or feature engineering: Select and transform the most relevant variables (features)
- Model selection & training: choose an algorithm and train it on your data
- Model evaluation: Test the model's performance on unseen data.
- Tuning & Deployment: fine-tune the model and deploy it for real-world use.

#### The python ML Ecosystem
- Python: The de facto language for machine learning due to its simplicity and extensive libraries
- Jupyter Notebooks/Google Colab: For interactive development and experimentation 
- Core libraries:
	- NumPy: For efficient numerical computation vectors, matrices
	- Pandas: For data manipulation and analysis (dataframes)
	- MatPlotLib/Seaborn: For data visualisation
	- Scikit-learn: The workhorse for classical machine learning algoritms
# References