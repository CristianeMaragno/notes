
Introduction/intuition to BM

  

Boltzmann machine are unsupervised learning algorithms used for recommender systems. All of the models previously presented are directed models, there is a direction in which the model operates. That’s is where the BM are different and stand out, they are undirected models, they don’t have a direction, the connections go both ways.

  

![](https://lh4.googleusercontent.com/guwWgw_05lgRZKa_ZX-QoYqQFq1LS0pv5qdwA4Il_jIOEglcw7AQJ8fCOkBstobgkC8_arP4DXO05_MKlNVDGtvDJNR_qvBx6SkBsJviEGlv-CeGrsLOCsTZPS0zA0VRavWkSTjSVEmeOmU6RF6H)

  

Boltzmann machines are fundamentally different to all other algorithms it doesn't have an output layer, are hyper connected, the connections are bidirectional and the visible nodes(nodes of input data) are connected with each other.  They don't just expect input data. What they do is they generate data. They generate information in all of these nodes, regardless of whether there's and input node or a hidden node. For a Boltzmann machine, it doesn't distinguish between these nodes. That's just for us. For a Boltzmann machine this whole thing is working with it's a system, it's generating states of this system.

Example of Geoffrey Hinton of a nuclear power plant:

![](https://lh3.googleusercontent.com/yxeNqgRQl4TfxFv0SFYuI9LYJi28tXcWfD_152GfIUGHT6GkgwSlDf_B1HslPZnK9QvLR9avRJK11do2qb5eJDjBpSmbBxB7Y6RYdS1nt1BeALvft6emIjCfwo3ktPjS7_jQhIsVdngVtB3RRpLy)

Think of a nuclear power plant, let's say that there are certain things that we can measure about the status of the nuclear power plant. So for instance, an important parameter that we should be measuring is the temperature inside the containment unit.Then, for example, we could be measuring how quickly a certain turbine is spinning. Also, we could be measuring the speed of the wind, the moisture of the ground, etc.

So there can also be lots of different parameters of the nuclear power plant that we're not measuring, but at the same time all these parameters all together, they all form one system and they all work together, and that is what the Boltzmann machine represents.

The Boltzmann machine is a representation of a certain system. In this case, a nuclear power plant, and the visible nodes are just merely things that we can and do measure, and the hidden nodes are things that we can't or don't measure.

The way this whole model works is that, instead of just waiting for us to input values for it to model the states, what it does is the Boltzmann machine is capable of generating all of the values. In our case what does that mean? It just generates different states of our system. So basically it looks at one state, and then it looks at another state and then it says, okay what if the temperatures higher, the wind is faster, the pressure in the pump is lower, the moisture of the earth is lower or higher compared to a state where those informations are different?

That is the essence of why it's not a deterministic deep learning model, it's a stochastic deep learning model or also, a better way to call it is a generative deep learning model because it generates these states.

we've got this system or this machine that describes our different states of our system. What we want, is we want to use our training data. We want to feed it into this Boltzmann machine as the inputs to help it adjust the weights of this system accordingly, It learns how, what are the possible connections between all of these parameters. How do they influence each other and therefore, it becomes a system, a machine that represents specifically our system in.

Once we've done the learning, we can use the Boltzmann machine to, for example, in the case of a nuclear plant, to monitor our nuclear power plant. Because we've modeled it using good behavior, behavior that hasn't led to any meltdown or any explosions, we know what is normal for the nuclear power plant. Then the Boltzmann machine will help us understand what is abnormal behavior. You cannot really model a nuclear meltdown through supervised learning because you'd have to have an example of a nuclear meltdown on that power plant

We don't have an output layer because we're not outputting any value. We are creating a model that describes our system.

At the same time, why all of these nodes are interconnected because as we kind of could sense from the diagram, all of these parameters are possibly interconnected with each other. We cannot deprive the system of being able to connect the speed of the turbine with, for instance, the moisture in the air on that day. So, it will decide for itself if there's a connection and how strong that connection is.

The directionality that the important thing to understand there is that for us, these are visible nodes and these are hidden nodes. For a Boltzmann machine, all of the nodes are equal.

Restricted BMs

We've got the standard Boltzmann machine or the full Boltzmann machine, and while in theory this is a great model and it's probably you can solve lots of different problems, in practice it's very hard to implement. In fact, at some point we'll run into a roadblock because we cannot, simply cannot compute a full Boltzmann machine and the reason for that is as you increase number of nodes, the number of connections between them grows exponentially. So therefore, a different type of architecture was proposed which is called the restricted Boltzmann machine

![](https://lh3.googleusercontent.com/Hr0MXGw0K2UkN1w1xP3uPPAWInP9S857VniLsX6HyItYkqsVPjQZ5wrKXkCEWUWc0MeQ8cR0qfdTFxaDODBF2N-D91O0WmU6EyzLw0WYyBLRtBf_8gtkDYz6IzZpCFx2AJWVkQeHwMj5QI4D0rKD)

So here we've got exactly the same concept with the simple restriction that hidden nodes cannot connect to each other and visible nodes cannot connect to each other. Other than that, everything's the same. We've got connections which are undirected meaning that they happen in both ways both from visible nodes to hidden nodes and from hidden nodes to visible nodes.

So let's say our restricted Boltzmann machine is going or our recommender system is going to be working on six movies.

As you remember, a Boltzmann machine is a generative type of model so it always constantly generates or is capable of generating different states of our system and then in training through feeding it training data and through a process called contrastive divergence we help the Boltzmann machine to become a representation of our specific system. Rather being a recommender system for any kind of possible impossible movies or any kind of recommender possible impossible recommender system, we make it become more and more like the recommender system that is associated with our specific set of movies that we are feeding into this system and with our specific training data.

What this restricted Boltzmann machine is going to learn is it's going to understand how to allocate its hidden nodes to certain features. And this process is very similar to what we discussed in the convolutional neural networks. So for example, through the training process, the restricted Boltzmann machine might identify that genres of movies are important features for instance, and the important thing to understand here is that it doesn't know that these are genres, it's just identifying certain features.

An important features may include an actor, maybe Kevin Costner, an award maybe an Oscar, a director, Robert Zemeckis. So, it will identify that these are important features Well let's go through this, during the training process, we're feeding in lots and lots of rows to the restricted Boltzmann machine and for example,these rows could have movies as columns and then the users as rows.

On a movie recommender system, we could get the ratings or the feedback that each user has left for the movie whether they liked it, that's a one or they didn't like it, a zero and also the empty cells means that person hasn't watched that movie. And, through this process this restricted Boltzmann machine what it is able to understand better our system and it is better to adjust itself to be a better representation of our system, and understand and reflect better all of the intra connectivity that is, that might be present here because ultimately, people have biases, people have preferences, people have tastes and that is what is reflected in the datas.

If somebody liked Movie two and three and didn't like Movie one just means that that's what's their preferences. Somebody else might have liked movie you one and might have not liked Movie two and might have liked that Movie three.

The BM associates features that thinks that are important and leaves a node that watches for that certain feature, so it activates when that feature is meet when trying to predict the likes of someone. Could be useful to think of it as in the convolutional neural network analogy. In there, we would feed in a picture into our convolutional neural network and it would, certain features would highlight if they're present in that picture.

Same thing here we're feeding in a row into our restricted Boltzmann machine and certain features are going to light up if they are present in this user's tastes and preferences and likes and biases.

What the Boltzmann machine does is it accept values into the hidden nodes and then it tries to reconstruct your inputs based on those hidden nodes. if during training if the reconstruction is incorrect then everything is adjusted the weights are adjusted and then we reconstruct again and again.

In a test, we are inputting a certain row and we want to get our predictions. So basically, there is not gonna be any adjusting of weights. We're just going to see how the Boltzmann machine basically reconstructs these rows.

Contrastive Divergence

Contrastive Divergence is the algorithm that actually allows Restricted Boltzmann Machines to learn, is a specific part of the learning process.

We learnt previously that Restricted Boltzmann Machines are feed different values, and it looks at them and looks for features and then assign certain nodes to those features to further understand our system and better represent our system. But the question that we still have is, how does the Restricted Boltzmann Machines adjust its weights. Because previously in the other neural networks that we've looked at, we had the gradient descent process, which allowed us to back propagate the error through the network, and therefore adjust the weights accordingly to minimize that error. But in this time, we don't have a directed network. We have an undirected network. And the question is, how do the weights get adjusted here. And this is where the Contrastive Divergence comes in.

![](https://lh3.googleusercontent.com/lgFVjMlQNzx9CGz91EPyjGiukxFYvxpAHOibDm1gzYDOey7fDpBlpP9BtlR32catVQOi8Vc1KKU2_fCHSYRDgPEXh8ENCfzPx645pEkeyRH_0IkxH_83goTfp4G-r6G3AGgdOaPQ4AI7SPaXuzzO)

So here we've got our input nodes in blue/purple. Once you put them into the network, using some randomly assigned weights, at the very start, the system or the Restricted Boltzmann Machine calculates the hidden nodes in red/blue. Then what's going to happen is those hidden nodes are going to use the exact same weights to calculate the input nodes, or to reconstruct, the input nodes. The key point here is that they weigh is exactly the same, they don't change. What is also important to understand is that the reconstructed inputs are not going to equal the original inputs even though the weight is the same.

![](https://lh5.googleusercontent.com/rYBd98xv8Mot_BZJxUhz3Us-ht9s2QD9wYi3aJlOzanfAzfwrgT5mu2po2o60Y3iFqjMpvX2uhp0ahzFV1FNfwtqW0dDMERZkUAQ_gCR45LQazWJhH4SPnLGgv0R4pFDC9M5WbSVoNXIZJsnljWQ)

  

The question is, once we've reconstructed are visible nodes, how come they're not identical to the original visible nodes even though we're using the same weights?

The reason for that is because these nodes are not initially interconnected, not necessarily is there a specific connection between them. 

Let's look at node number two over. How does it get reconstructed? Well, it gets reconstructed based on the values that all of these five hidden nodes have in them. So once we first run this RBM, these initial values of the visible nodes will assign or will initiate some values in your hidden nodes. Then once we run it backwards, these hidden nodes will reconstruct, all of these visible nodes including this second node.

But the thing is, each one of the hidden nodes wasn't constructed just based on this second node. If that was the case, the value from this second node was used to create the value in all of the hidden nodes and then we ran everything backwards, then yes, this second node would be identical to what it was initially. But the way the RBM works is that each hidden node, during the forward pause, was constructed from all of the visible nodes.

So every single hidden node was constructed from all six visible nodes. And so therefore, all of these nodes have values that didn't initially come from just the second visible node. They came from the other visible nodes, and therefore when you reconstruct this second visible node even though using the same weights, the values in the hidden nodes came from other visible nodes as well and therefore the reconstructed value in the second visible node is not going to be equal to what you initially.

So there's a first forward pause(calculates the hidden layer) and backward pause(reconstruct the visible nodes), now we're going to do another one. We're going to again feed these values of the reconstructed node values of our inputs into the RBM and we're going to get some outputs or some hidden values. Then based on these hidden values, we're going to reconstruct the inputs again, and again, they're not going to equal. Then we're going to construct the hidden values and so on. And this whole process is called Gibbs sampling.

  

![](https://lh6.googleusercontent.com/vNtLptprwjyYe3MvW98PgWHKmS50Fpp0lKJkh09s_I1HSHFe6sOPLufClWkIIs8bmQa9_-Uepcr7zoZk872hcXDn8qSX55oF1Fdg4w17-QBqxOlTW1PtJGqc-i1ddUQy3hWusM53glkILU-uFDwE)

And towards the end, finally, at some point, we're going to get some reconstructed input values which are such that when we feed them into the RBM, and then we try to reconstruct them again, we will get those same values.

So in this final scenario, what happens is yes, our network is modeling exactly our inputs. So basically, we can input in and we will always get the output. So in essence, this process has finally converged and our network is finally a great model to model our inputs. To model that specific input.

And remember, through this whole process, the weights were constant.

---------------------------------------------------------

The formula presented below show how the weights affect the log probability. How changing the weights will change the log probability, and the way it'll change the energy curve.

  

![](https://lh5.googleusercontent.com/Pp9WsXgJ9K3Yq1BfRygbKtRPKWE96fciFIJmm0TCv2s4obs8rdHzLEd9cSQk4CGedHxtTZM1CGYwHyB82iIHIfg0Wl4PwM9H8MsRSkxwAeYsgVC1_iJlTMBxBqDM0-3f7b_tdTJh4vSi7Psg1Nig)

  

Let's talk about the energy. Where does the energy come from? We've talked about energy based systems and we said that in the Restricted Boltzmann Machines the way we define energy is through weights. So the weights are fixed as we saw through the whole previous process the way to fixed, and we're going to define

So our first pause through the RBM and that's where we happen to be, just because the weights are initialized randomly. For example, we end up somewhere like where the green ball is. After, what happens is we end up somewhere where the red ball is (hidden layer). 

A system which is governed by its energy will always try to end up in the lowest energy state possible. So as you can see, this ball is rolling towards the bottom of the curve. And that's exactly what's happening through that divergent process, through that process which we discussed through our diagrams as we go through the Contrastive Divergence process basically. What's happening is, we're going closer and closer to our lowest energy state.

You can use the example of the gas. You have a room and then you let out some gas in one corner. For instance, if you got a big room, and then you let out some gas in the top right corner, just based on the architecture of the room based on the conditions that the gas has been put into, hence the weights. So the the architecture of the room or the design of the room, that is not the lowest energy state for that gas at that point in time. So the gas could be in a much lower energy state than that. And so what the gas starts doing is it starts expanding into the whole room, this is what happens with our model.

Through the Contrastive Divergence process, we're finding what's the values in our system, the inputs and the hidden layers, what they should be for the system to be in the lowest energy state possible. 

And from there, what that formula is telling us is, once you have that lowest energy state, once your ball is on the bottom part of the curve, basically if you subtract the first value from the second value after the equal, it will tell you how adjusting your weights will affect the log probability of the system being in this state.

So basically, this is a recipe, this formula is a recipe for adjusting your curve for shifting or for modifying your energy curve, so that you can make sure that this state is inside an energy minimum, so that you can get any desired effect.

So this is a long process, as you can imagine it takes very long. But in 1998, Jeffrey Hinton discovered a shortcut. What happens is he says that, "Even if you take just the first two pauses", you don't wait until it convergences to the end, "This is sufficient to understand how to adjust your curve as far as is the initial stage."

So this is a CD one, Contrastive Divergence one pause. So if you do a CD one,  what happens is, your green ball is over here, your red ball is over here and you know that and that's enough for you to know which way is rolling. So like similar to what we had in gradient descent that's why it's downhill. But you now want to adjust your curve. In gradient decent we just had a curve and we were like finding the minimum.

Here we have control over the curve, we are adjusting the weights because it's an energy based process we're adjusting the weights so that minimum is actually going to be here rather than here. So let's look at that. So we know that the balls are going rolling downhill. So what we actually want is want to pull this curve down on the point where our green ball is and we want to push it up where our red ball was.

![](https://lh4.googleusercontent.com/g8tURmgnqg0hkyN5fcEiojQUaYPMBAxerw0fKfl_37HdtcCfiYJ6HyS6WhAm2j3xeEz6hLQxt5sqZIBk9GQfCKXoanoD02MyQKUm-aQ1CIXS7xdilTjupj2tW68E77ypXsPy093ZY779CTnvPGdd)

So you can see your ball is already inside the minimum, and that way you don't even have to go through the long process of sampling to get to that recipe of how to adjust the curve, but you can just adjust the weights.

We have an energy curve and the shape of this energy curve, is governed by the weights in the system, that's just how we design it. We also know that the way we've designed the system, is that the Restricted Boltzmann Machine, will aim to always get to the minimal energy state, the state with the minimal energy possible.

And what do we mean by get to that state? What's the process of getting to that state? Well, that process we just looked at that sampling that Gibbs sampling process, where we input the inputs then we get the hidden values and where we construct the inputs then we get the hidden values, reconstruct inputs and so on.

Through that process, the system will always aim to get to values and its nodes which represent the lowest energy state possible. Now, what we want is we want to redesign the system hence, redesign the energy curve, so that the energy curve reflects also that the system is such that when we input our values, our training values, the system is already going to be in the lowest energy possible. 

There's a shortcut that we don't actually have to go through to the very end of the sampling process, we can just do two pauses, we go first pause, second pause and so we do a CD one, Contrastive Divergence one, and that will tell us how to adjust the curve.

---------------------------------------------------------------------------------------------------------------------

  
  

conda install -c pytorch pytorch

  
  
  
  
  
  
  
  
  
  
**