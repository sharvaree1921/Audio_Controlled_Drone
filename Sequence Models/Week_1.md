## Week 1: Recurrent Neural Networks

### Why Sequence Models?
RNN are used in Speech Processing, Natural Language Processing, Chatbots, Music Recognition, Machine Translation, etc.
Usually the input data is the sequence data. 

Some Examples where sequence models are used:
- Music Generation
- DNA Sequence Analysis
- Sentiment Analysis
- Video Activity Recognition
- Name entity recognition
- Machine Translation

The input X and output Y can have same or different lengths. Both can simultaneously be sequential or either of them could be sequential.

### Notation
Let's consider an example: Name-entity recognaition.

Consider the sentence: "Harry Potter and Hermoine Granger invented a new spell"
This input sentence contains 9 words and hence 9 input features denoted by x^{1}, x^{2},...,x{t},...,x^{9}.
For entity recognition, it is "Harry Potter", "Hermoine Granger". Hence the output sequence is {1, 1, 0, 1, 1, 0, 0, 0, 0} which is denoted by y^{1}, y^{2},...,y{t},...,y^{9}.

T_x = 9, T_y = 9 which is length of input and output data. Coincidently, it is equal in this case.

Also, each training example is denoted by x^{i}. Hence, the t-th feature of the i-th training input is given by x^{i}{t}. Similarly y^{i}{t}.
Similarly, T_x^{i} and T_y^{i} are input and output lengths of the i-th training sample.
  
![notation-1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2015-39-12.png)  
  
**How do we represent individual words of a sentence in NLP?**

Vocabulory. Given a dictionary size of say 10,000.(Usually it's 30,000/50,000)
Use one hot encoding for the dictionary array for representating each word in the given sentence. 
  
![notation-2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2015-43-50.png)

### Recurrent Neural Networks

Observe that, the input and output lengths of the training samples could be variable. Also, the word appearing at initial part of the sentence may have significance important at its later part. Thus, the NN needs to memorize across all theprevious layers.

Note that, the input data x^{1}, x^{2},... etc. are 10,000 sized one-hot encoded large vectors. Thus the no. of parameters are drastically increased. 

![RNN-1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2015-54-06.png)

All these disadvantages are overcome by the RNNs. In RNN, the current time step gets two inputs: the current stage input and the output of the previous time step i.e. the activation of previous step. The diagram at the right is the rolled/compressed version of the RNN.

The parameters governing the i/p and o/p connections are goverened by W_ax whereas the activations that are the horizontal connections are goverened by W_ax. These are shared parameters.

![RNN-2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2016-13-46.png)

Forward Propagation: We calculate the output Y as well as the activation of that particular time step. Depending upon the desire, we choose the appropriate activation functions such as ReLU(for avoiding vanishing gradients), Sigmoid(for binary classification)

![RNN-3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2016-19-09.png)
 
Simplified RNN notation can be seen as follows:

![RNN-4](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2015-54-06.png)

### Backpropagation in RNN

The activations depend upon parameters W_a, b_a. To compute Y_hat, we need parameters W_y, b_y. We introduce the element wise loss(i.e. for single word), called as standard logistic regrssion or the cross entropy loss. Adding the corresponding losses we get the total loss.

![Back](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2017-18-48.png)

### Different Types of RNN

There could be various types of input and output data types. T_x and T_y can be equal or not-equal.

![rnn](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2021-41-14.png)
![rnn-1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2021-46-46.png)
![rnn-2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2021-48-02.png)

### Language Model and Sequence Generation
Given any sentence, the language model tells about the probability of that particular sentence of the complete sentence. The probabilities are calculated for each word sequentially. The output of previous step is fed as an input to the next time step.

![LM](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2021-59-06.png)
![LM-2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2022-07-56.png)
![LM-3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot from 2021-05-19 22-14-34.png)



























