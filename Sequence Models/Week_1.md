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
EOS means End of Sentence. 

Given any sentence, the language model tells about the probability of that particular sentence of the complete sentence. The probabilities are calculated for each word sequentially. The output of previous step is fed as an input to the next time step.

![LM](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2021-59-06.png)
![LM-2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2022-07-56.png)
![LM-3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2022-14-34.png)

### Sampling Novel Sequences
![samp](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2022-58-39.png)
**Character Level Language Model**
Assign various characters, punctuation_marks to a vocabulory. When character level model is used, different characters are assigned different <y^> values. Now our training data would be individual characters rather than words. We don't have to worry about the unknown word tokens. The words like 'mau' are assigned non-zero pobabilities now. Whereas if mau was not in your vocabulary for the word level language model,you just have to assign it the unknown word token. One disadvantage is that, you get a much longer sequence. Hence, computationally heavy.

![samp2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2023-09-38.png)
![samp3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2023-12-06.png)

### Vanishing Gradients with RNNs
Language can have a long term dependencies. See the two examples in the image. Vanishing Gradients can occur while forward prop. or backprop. The neural Network may find it difficult to memorize the features(say a singular noun or the plural noun). Thus the output is greatly influenced by the near by previous layers. 
The gradients can also increase exponentially. However, the exploding gradients problem can be spotted more quickly. Gradient clipping is one of the way to avoid this exploding gradient problem. But, vanishing gradient is more important problem to tackle. 

![VG](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-19%2023-22-25.png)

In order to capture much larger range dependencies and overcome the problem of Vanishig gradient, _Gated Recurrent Units_ are introduced.

### Gated Recurrent Unit(GRU)

Complete video [here](https://www.coursera.org/learn/nlp-sequence-models/lecture/agZiL/gated-recurrent-unit-gru)

We introduce a new variable called as c^<t> which acts as memory cell(say it memorizes whether the subject of the sentence is singular or plural). This memory cell is equated to the activation function. At every time step we are going to overwrite this memory cell with a value of c_tilda^<t>. So, c_tilda^<t> is going to be candidate for replacing c^<t>. 
  
Now, we introduce the concept of gate called as Gamma_u which is important concept of GRU. It's called the update gate and its value lies between 0 and 1. Since, sigmoid function is used while its computation, for most of the values, its vale is 0 or 1. The key part of the GRU is this equation which is that we have come up with a candidate where we're thinking of updating c using c tilde, and then the gate will decide whether or not we actually update it. And so the way to think about it is maybe this memory cell c is going to be set to either zero or one depending on whether the word you are considering, really the subject of the sentence is singular or plural.
So because it's singular, let's say that we set this to one. And if it was plural, maybe we would set this to zero, and then the GRU unit would memorize the value of the c<t> all the way until here, where this is still equal to one and so that tells it, oh, it's singular so use the choice was.
And the job of the gate, of gamma u, is to decide when do you update these values. 

![gru1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2013-21-23.png)  
  
if the update value,
this equal to one, then it's saying
set the new value of c<t> equal to this candidate value.
So that's like over here,
set gate equal to one so go ahead and update that bit.
And then for all of these values in the middle,
you should have the gate equals zero.
So this is saying don't update it,
don't update it, don't update it,
just hang onto the old value.
Because if gamma u is equal to zero,
then this would be zero,
and this would be one.
And so it's just setting c<t> equal to the old value,
even as you scan the sentence from left to right.
So when the gate is equal to zero,
we're saying don't update it,
don't update it, just hang on to the value and don't forget what this value was.
And so that way even when you get all the way down here,
hopefully you've just been setting c<t> equals c<t> minus one all along.
And it still memorizes,
the cat was singular. 

![gru2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2013-32-20.png)  

**Note that when gamma_u is zero or close to zero, the c^<t> equation still contains the term c^<t-1>. This implies that, it still memorizes the previous value and thus overcame the problem of vanishing gradient. 
  
In full GRU, the 'r' stands for how relevant that previous activation or memory cell is.
  
![gru3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2013-41-45.png)

**Correction**  
![gru4](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2014-15-54.png)  

### Long Short Term Memory(LSTM)

LSTM is much more powerful than GRU. GRU had gamma_u and (1-gamma_u) as the update and forget gates respectively. However, LSTM itself introduces its own separate forget gate called as gamma_f. Also, gamma_o i.e the output gate is also introduced for obtaining the output. Now we have 3 gates instead of 2 gates in GRU. The equations governing the LSTM are as follows:

![lstm1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2014-30-23.png)
![lstm2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2014-35-49.png)
**Correction:**
![lstm3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/vEHtd8hlEemS6xJ43HxpzA_8c54dc2a23799817e45bd4fb6fe96389_Screen-Shot-2019-08-26-at-5.56.30-PM.png)
There exist various variations to the existing LSTM. The gate values may also depend upon x_t, a_(t-1), or other previous layer activations instead of just the previous layer values. This type of LSTM is called _Peephole Connection_
  
When to use GRU or LSTM?
GRU were introduced much later in the research. The advantage of GRU is that it is simplified version and can be used in huge networks. It's computationally also good. However, LSTM networks are much more powerful and are used historically. 
 
![gru and lstm](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/1*yBXV9o5q7L_CvY7quJt3WQ.png)
  
### Bidirectional RNN
  
By now, we have seen only the basic structures of RNNs. However, there are two ideas which build more powerful RNNs namely: Bidirectional RNN(which allows one to access the information fromprevious or later instants) and Deep RNNs
  
In BRNN, we will introduce the backward connections in between the existing layers.

![brnn1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2014-50-55.png)
![brnn2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-20%2014-55-18.png)  
  
This is
a modification they can make to the basic RNN architecture or the GRU or the LSTM,
and by making this change you can have a model that
uses RNN and or GRU or LSTM and is able to make
predictions anywhere even in the middle of a sequence by taking into
account information potentially from the entire sequence.
The disadvantage of the bidirectional RNN is that you do
need the entire sequence of data before you can make predictions anywhere.
So, for example, if you're building a speech recognition system,
then the BRNN will let you take into account
the entire speech utterance but if you use this straightforward implementation,
you need to wait for the person to stop talking to get
the entire utterance before you can
actually process it and make a speech recognition prediction.
So for a real type speech recognition applications,
they're somewhat more complex modules as well rather than just
using the standard bidirectional RNN as you've seen here.
But for a lot of natural language processing applications where
you can get the entire sentence all the same time,
the standard BRNN algorithm is actually very effective. 
  
### Deep RNN
Complete Video can be found [here](https://www.coursera.org/learn/nlp-sequence-models/lecture/ehs0S/deep-rnns)
  



















