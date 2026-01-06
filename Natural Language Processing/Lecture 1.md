>Machines need World knowledge

## Modalities

- Homeworks -> GItHub Classroom
- Learn **PyTorch**, **Transformers**
- Homeworks -> let Unit Test pass ✅
- and assignments will increase in difficulty
- first-weeks -> one week assignment
- last-weeks -> multi-week assignments

- Submit **every** homework even if empty sheet
- 5 points on average
- final exam 90mins - write pseudo code (python) - english
- one does not have to commit to one exercise group

# Build Sentiment Classifier (Binary)

> Task: Classify the overall sentiment if it is positive or negative

Q1: For what does we need that?
	- Product Rewievs
	- Analyse political analysis
	- Prioritising support tickets

Q2: Why only two classes?
	- beacuse we trained it so
	- we could also have multiple ones (3, 5, ...)
	
Other use cases: Offensive lang. detection, Intent Detection, Mediacal Coding

## 1 Layer NN for Classification

⚠️ Repeat basic analysis
Matrix: A * B != B * A

> Linear Transformation of Vectors that represents a output (neg/positive)

- Represent text as vector
- Matrix Multiplication is big part of it

We do #affine-Transformation
	- Matrix Multiplication + bias vector
	- **f(x) = Wx +b = y**
	- y = output vector
	- W = Matrix
	- b= bias vector
	- x = input vector

after that: #activation

## Vectorisation

- How text into vectors
- One approcach One-hot-encodeing
- in exercise work with one hot encodings
	- create dictionary
	- and after that map vectors to text
- impossible to represent all words as a one hot
- Count vectorization
	- add up all one hot vectorized words in a text
	- disadv. we lose order of words

## Activation Functions

- regression
	- predict numerical value
	-  percentage...
	- how positive/negative
	- and just transform into a scalar (Nummer) here activation func just identity function

- Argmax function
- Softmax function
	- single label prediction problems
- Sigmoid function
	- might not produce "one hot" rather ,,multi-hot"

Single Label Classification
	- either or

