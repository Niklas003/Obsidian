## Learnable Parameters
E.g.
- Weights 
- Bias Terms
**PRÜFUNGSRELEVANT**

Ho to learn params (weights) that forward path makes sense?
-> Almost no NLP more model training

- Use 1 Layer Network

- Training Data in form of labeld data (pos/neg labeld)
- Use Train Data to learn weights
- > Goal to "fit" the model at least for this data points
## SGD Stochastic gradient descend

- random init of all params in the network
- and then > how well does it work
- compute changes that need to make 
- do the change 
- repeat

Do this in two steps:
1. Compute the "Ableitung" of the loss in respect to the parameters to see the magnitude 
2. Adjust the parameters

>The first step computes the gradient of the loss function at the current position. This determines the uphill directionof the loss function. The second step moves a small distance α downhill (hence the negative sign).The parameter α may befixed (in which case,we call it a learning rate), or we may perform a line search where we try several valuesofαtofindtheonethatmostdecreasestheloss. Attheminimumof theloss function, thesurfacemustbeflat(orwecouldimprove furtherbygoingdownhill).Hence,thegradientwillbezero,andtheparameterswillstop changing. Inpractice,wemonitorthegradientmagnitudeandterminatethealgorithm whenitbecomestoosmall.

backward pass:
- check how much does every weight contribute to an error
- by going back in the model

Epoch/Epoche: number of times that you have seen the full training data
- You backpropage after each minibatch (certain set of datasets part of dataset)
- Why do epochs exists: just a stopping criteria when to stop training

## Lossfunction

### Cross entropy loss
Most common loss function
function to determine how correct or incorrect the model is. 

standard loss x² per unit

"punishing the model more"
## Loss landscape

2 D für einen Wert 
3D für 2 Werte 
can be plottet
- there is a minimum in the plot. This minimum might be the bist value for the param


which loss function typically used?
- cross entropy loss
- mean squared for regression

What happens if we set learning rate to high in SGD?
- increases rist thta weight update worsens our loss

What is the primary purpose of the dev (validation) set?
- Tune the hyperparameterns