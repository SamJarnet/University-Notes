2026-01-01 17:40

Status:

Tags: [[Artificial Intelligence]]


# Natural Language Processing


#### What is NLP? NLU? LM? LLM? LMM?
- NLP: Natural Language Processing
- NLU: Natural Language Understanding
- LM: Language model
- LLM: Large Language model
- LMM: Large Multimodal model
- NLP is a broad term that encompasses all things computers + language (both understanding and generating): e.g. speech recognition, language translation, sentiment analysis, and text summarisation , etc.

#### Classical NLP vs NLP of today 
- Many topics in "classical" NLP are things like:
	- Statistical language modelling
	- Word embeddings (word2vec) 
	- Syntax 
	- Semantics
	- Tagging
	- PCFG

#### Language Modelling 
- In general: language modelling task is assigning probability to text
- Assume finite vocabulary of words V = {these, are, examples. words}
- We can construct an infinite set of strings $V^*$ = {these are, these example, ...}
- Given training set of sample strings: {$s_1, s_2, ..., s_n | s_i \in V^*$}
- Estimate probability distribution p: V* $\rightarrow \mathbb{R}$ 
	- ![[Pasted image 20260101174909.png]]

#### Why model language?
 - Many application areas including:
	 - Autocomplete 
	 - Auto-correct
	 - Machine translation
	 - Code completion
	 - Chatbots

#### Unigram language model (Bag of Words BoW)
- Sentences are finite with a "STOP" token, vocab becomes:
	- $V' = V \cup$ {STOP}
- Each word generated with prop $q(x_i)$
	- ![[Pasted image 20260101175115.png]]
- Generative? keep picking words until "STOP" is chosen
- 0th order markov model (order of words doesn't matter hence bag of words)

#### Bigram language model
- 1st order markov model: each word depends only on it's predecessor 
- ![[Pasted image 20260101175227.png]]

#### N-gram language models
- Each word depends on N -1 predecessors 
- ![[Pasted image 20260101175306.png]]
- Example of tri-gram
	- ![[Pasted image 20260101175324.png]]

- As N increases performance on training data goes up, but overfits quickly 
- Text becomes more fluent as N increases
- Careful balance 
- Empirically a tri-gram can get you pretty far

#### How to evaluate LM performance?
- Likelihood: Probability of data under the model 
	- ![[Pasted image 20260101175532.png]]
- (Negative) log likelihood: log of probability of data with respect to model 
	- ![[Pasted image 20260101175617.png]]
- Perplexity: inverse probability of data, normalised by number of words (or tokens)
	- ![[Pasted image 20260101175650.png]]
- Goal: Find model that maximises likelihood on training set:
	- ![[Pasted image 20260101175710.png]]

#### Optimising all three metrics are equivalent 
- ![[Pasted image 20260101175735.png]]
- Minimising cross entropy is equivalent to minimising negative log likelihood 
- Perplexity is just the exponentiated cross entropy 
- What is perplexity?
	- Measure of models uncertainty or surprise when predicting next word
		- Low perplexity -> better performance 
	- Also, can be thought of as the average branching factor of a language 
		- e.g. if a model has perplexity 10, this means on average, each word in the sequence could be followed by 10 equally likely words
- Example:
	- ![[Pasted image 20260101180038.png]]

#### What is an LLM?
- They are large language models built on the transformer architecture with $~O(10B)$ parameters trained on internet scale data
- ]There are many forms/stages to LLM training and usage
- Proprietary models outperform open source ones, but they are catching up
- These things cost many millions of dollars to train and a lot of compute and time 

- Just two files on your OS
- Some parameters file (weights and biases) + execution code
- Common forms:
	- GPT (Generative Pre-trained Transformer)
	- BERT (Bidirectional Encoder Representations from Transformers)

#### Step 1: collect internet scale data
- mixture of high low quality (high volume) and high quality (lower volume) data
- Sample the datasets

#### Step 2: Tokenisation 
![[Pasted image 20260101180724.png]]

- The outcome of pre-training is a base-model
- Base models are just document completion robots
	- They are not trained for any specific task in mind, they just fill the most likely next word

#### We supervise fine tune base models
- Supervise fine tuning is a critical step to making an assistant model
- Human vendors annotate data according to guidelines written by other humans 
- This is usually very low volume but very high quality
- Then we finetune the model on this dataset
- 1 day to days training time 
- This makes the model able to complete a task such as text classification or Q&A much better than the base model

#### The last Step is RLHF
- Comprised of two steps:
	- Reward modelling: which answer do you prefer?
		- Easier to identify good outputs than generate them
	- Reinforcement learning step: maximise the reward function you found
	- Usually works a lot better

#### How to make better LLMs?
- LLMs seem to follow scaling laws 
	- N number of parameters in the network
	- D the amount of text we train on
- We get better models by scaling 
	- Compute 
	- Data
- This is one way to get better LLMs 
	- Modelling improvements exist too 
		- Just a bit harder than usual 

#### A closer look at the Transformer
- Encoder processes the input sequence, creates a representation of it 
- Decoder uses the representation + target sequence to generate the output 
	- Recursive in nature, one token at a time, using encoder info + the previously generated tokens 
- Attention: Allows for capturing long-range dependencies in the data

#### You don't need both 
- Encoder-decoder Transformer is useful for tasks like machine translation (seq2seq tasks) 
- However, you can have encoder-only transformers and decoder-only transformers 
- Encoder-only Transformer: BERT
	- Useful for things like text classifications, NER, QA, (focus on understanding input)
- Decoder-only Transformer: GPT
	- Useful for generating text & trained with LM objective

#### Not just text
- We can use Transformers across all fields of AI
- Computer vision, NLP, RL, Speech, Translation, Graphs/Science (e.g. AlphaFold)
- These fields use to have little overlap, very specialised architectures, etc.
- We are at a interesting point where AI architectures are seemingly converging 
- Roughly just chop up your input sequence (image into squares, etc) and feed into the transformer and it just works ?
# References