
O que são?

  

Kohonen Self Organising Feature Maps, or SOMs, provide a way of representing multidimensional data in much lower dimensional spaces - usually one or two dimensions. This process, of reducing the dimensionality of vectors, is essentially a data compression technique known as vector quantisation. In addition, the Kohonen technique creates a network that stores information in such a way that any topological relationships within the training set are maintained

.![](https://lh3.googleusercontent.com/kkwS8uTP1vlTAGFAJO98La8hBaUlue_jRlPvNirZZuPxqnigwGXbZx8UQ9m493LIbIvApv8ee4kvWphF8AaobpMdDVbPrXYyOyhRfHGKph9d6fUgcgDeJv5lpgl4b9ifzczl529j5y3gez0jrOrA)

U.S. Congress voting patterns

  

Reviewing, with supervised learning, an input vector is presented to the network (typically a multilayer feedforward network) and the output is compared with the target vector. If they differ, the weights of the network are altered slightly to reduce the error in the output and this process is repeated. SOMs learn to classify data without any external supervision, with no no target vector. 

  

One thing to be aware is that If you try to think of SOMs in terms of neurons, activation functions and feedforward/recurrent connections you're likely to grow confused quickly. The concepts that might have the same names have different meanings from the knowledge of supervised learning.

  

Como funciona

  
![](https://lh5.googleusercontent.com/u-BW0YZ1s4HHIbCR_N3jdJX1xF2s5LJet0gCQ4fYXcKvZD8z5l6WdZ0erfHKzt_DKx2arRc0ShqcY1UT4lF-8c8z2y4XyZkHhgnn6SWw4Zkd_IgyDawWshMtYS_Bd8uZ3Xdrs6O3_DwN_iqnX_pe)

![](https://lh6.googleusercontent.com/5wxoFzEpx_Wd0n0eFp5Hk2VWdO78lgUlAdALzlycntJBYPeSQheei1maMbfe67FDNmrP1NGoNhD8h59YoFLrkXJ--9eWop9im6Xd_2tu8FjDUWi3cbsPnCX9Hsu2tUO4xLkAhet-qqGgjzZbOLHy)

Here we have three features or three columns in our data set, so therefore, we might have thousands and thousands and thousands of rows, each of which has three columns.

And that means that our input data set is actually three dimensional, whereas our output data set in a self-organizing map is always a two-dimensional map, and therefore here we are reducing the dimensionality from 3D to 2D.

  

Each neuron will have a weight assigned to it. In artificial neural networks, weights were used to multiply, so we multiply the input of this node, or whatever we have in this node, by the weight, we added them up, and then we applied an activation function. Well, in self-organizing maps, there is no activation function. Weights are a characteristic of the node itself, are actually coordinates. 

  

Here you have one node representing a point in your input space, and again if you had 20 columns in your inputs, each node would have 20 weights. So, each one of the nodes, has its own weights at the start of the algorithm, as usually weights are assigned at random to values close to zero but not zero. And therefore each one of these nodes has its own imaginary place in the input space.

  

This is the core of the self-organizing map algorithm. Now we're going to have a competition. Among these nodes, we're going to go through each of our rows of our data set, and we're going to find out which of these nodes is closest to each of our rows in our data set. And we found that the closest one out of all of them them is node number three. And we're going to call node number three, BMU, or the best matching unit.

![](https://lh5.googleusercontent.com/XWKABCVFpZq3vDrpKt0bmwQ9BFFcgwQwlNEfoLMPuetM_ZWilNZcQUlRRsMyuCmD-TxtdUGCbLRKhzBIWq9ZtjbRcWukVusCNfwFBjuY4nhSY9dKomLC33tdOht7lBRKKA4byd5cUTBwlfDqTE0g)

  

So the weights are going to be updated for this best matching unit, so that it is actually even closer to our first row in our data set. What's happening is not just this one point is being dragged closer, but also some of the close, some of the nearby points are being dragged closer to this point.

  

![](https://lh6.googleusercontent.com/4X1uFgQMxyOODNcyAT_pNAA0Jvo9W8COeJTbI_qvYqVx_pJd6NIiiMp_YOdZhg5jKKKb2Y3N1pxTom3mEKzklnIaAmn7Kf--bUf66EBEDs8qaOHPjlrr6WdArZhJAR57DilXsHDr_jg5yZV2DPoE)

(OBS: Here we can see that there's some values that don't fall under the radius, that usually doesn't happen in self-organizing maps, this is just our visual example.)

And the way it works is the closer you are to the BMU, the heavier are the weights updated on a determined radius. So the closer you are to this BMU, the harder you will get pulled towards that row. So if, as example, there is a point that is nearer the green point than is from the yellow point, on the pull to that side and this side, it will end nearer the green point.

![](https://lh5.googleusercontent.com/u-BW0YZ1s4HHIbCR_N3jdJX1xF2s5LJet0gCQ4fYXcKvZD8z5l6WdZ0erfHKzt_DKx2arRc0ShqcY1UT4lF-8c8z2y4XyZkHhgnn6SWw4Zkd_IgyDawWshMtYS_Bd8uZ3Xdrs6O3_DwN_iqnX_pe)

Through the epochs  your radiuses actually shrink. So the process becomes more and more accurate as you go through your dataset again and again and again and if at the start you were just trying to get all of your SOMs very close to your data and roughly on the surface of your data, now you start to be more and more specific and targeted in your approach.

Summing up, each neuron compare their distance with the row and see witch of them are closer. So they update their position to be even closer and also update the position of the neurons on a certain radius (pull towards him).

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
![](https://lh6.googleusercontent.com/4X1uFgQMxyOODNcyAT_pNAA0Jvo9W8COeJTbI_qvYqVx_pJd6NIiiMp_YOdZhg5jKKKb2Y3N1pxTom3mEKzklnIaAmn7Kf--bUf66EBEDs8qaOHPjlrr6WdArZhJAR57DilXsHDr_jg5yZV2DPoE)  
![](https://lh6.googleusercontent.com/5wxoFzEpx_Wd0n0eFp5Hk2VWdO78lgUlAdALzlycntJBYPeSQheei1maMbfe67FDNmrP1NGoNhD8h59YoFLrkXJ--9eWop9im6Xd_2tu8FjDUWi3cbsPnCX9Hsu2tUO4xLkAhet-qqGgjzZbOLHy)![](https://lh3.googleusercontent.com/kkwS8uTP1vlTAGFAJO98La8hBaUlue_jRlPvNirZZuPxqnigwGXbZx8UQ9m493LIbIvApv8ee4kvWphF8AaobpMdDVbPrXYyOyhRfHGKph9d6fUgcgDeJv5lpgl4b9ifzczl529j5y3gez0jrOrA)  
  
  
![](https://lh5.googleusercontent.com/u-BW0YZ1s4HHIbCR_N3jdJX1xF2s5LJet0gCQ4fYXcKvZD8z5l6WdZ0erfHKzt_DKx2arRc0ShqcY1UT4lF-8c8z2y4XyZkHhgnn6SWw4Zkd_IgyDawWshMtYS_Bd8uZ3Xdrs6O3_DwN_iqnX_pe)

![](https://lh5.googleusercontent.com/XWKABCVFpZq3vDrpKt0bmwQ9BFFcgwQwlNEfoLMPuetM_ZWilNZcQUlRRsMyuCmD-TxtdUGCbLRKhzBIWq9ZtjbRcWukVusCNfwFBjuY4nhSY9dKomLC33tdOht7lBRKKA4byd5cUTBwlfDqTE0g)----------------------------------

  
  
  
  
**