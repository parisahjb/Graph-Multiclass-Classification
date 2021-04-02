# Graph-Multiclass-Classification
How to run classifier?
**The easiest way is Google colab: 
1.	Create a folder “graph” in your google drive including dataset.
2.	upload “Asgn1_GoogleColab.ipynb” from Google colab and run code.
**Just need to execute the following command on Google colab before running the main 
code:
pip install stellargraph

Quick overview of the model
All detailed explanation is provided in the code which is super easy to run on Google Colab.
*	Loading dataset
*	Creating node features with word2vec method from titles.txt
*	Node classification with directed GraphSAGE
*	Creating the GraphSAGE model in Keras
We need two other parameters, the batch_size to use for training and the number of nodes to sampl
e at each level of the model.
we choose a twolevel model with 100 nodes sampled in the first layer 50, and 50 in the second layer
.
*	A DirectedGraphSAGENodeGenerator object is required to send the node features in sampl
ed subgraphs to Keras
*	Using the generator.flow() method, we can create iterators over nodes that should be used to
 train, validate, or evaluate the model.
*	For training we use only the training nodes returned from our splitter and the target values. T
he shuffle=True argument is given to the flow method to improve training.
*	Now, we can specify our machine learning model, we need a few more parameters for this:

*	Layer_sizes is a list of hidden feature sizes of each layer in the model.The bias and dropout 
are internal parameters of the model.

*	graphsage_model = GraphSAGE(
*	    layer_sizes=[64, 32], generator=generator, bias=True, dropout=0.2,activations=["tanh","ta
nh"],
*	    aggregator=MaxPoolingAggregator)

*	Now, we create a model to predict the 20 categories using Keras softmax layers.

Training the model
*	Now let’s create the actual Keras model with the graph inputs x_inp provided by the graph_m
odel and outputs being the predictions from the softmax layer.
*	Now we have trained the model we can evaluate on the test set. Our test file doesn't have la
bels.
*	so I just write the code here but use val_gen again to see the accuracy. Then, I will predict la
bels of test nodes and will save the result.

Making predictions with the model
*	Now let’s get the predictions themselves for all nodes using another node iterator:
*	Node embeddings
*	Evaluate node embeddings as activations of the output of GraphSAGE layer stack, and visua
lise them, coloring nodes by their subject label.
*	The GraphSAGE embeddings are the output of the GraphSAGE layers, namely the x_out var
iable.
*	Let’s create a new model with the same inputs as we used previously x_inp but now the outp
ut is the embeddings rather than the predicted class.
*	Additionally note that the weights trained previously are kept in the new model.

** For illustration purpose, I used val.txt, but if the test.txt have lables, we can plot the test file easily.

** Final accuracy on val.txt file
Val Set Metrics:
	loss: 0.3213
	acc: 0.9052
