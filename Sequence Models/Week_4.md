## Transformers

### Transformers Network Intuition

**Must See [this](https://towardsdatascience.com/illustrated-guide-to-transformers-step-by-step-explanation-f74876522bc0) video and article.**

One of the very very important architectures in the NLP model.
Transformers Network allows you to compute all of these complicated complications in a parallel manner rather than sequentially from left to right as in RNN or LSTM.
RNN process one outtput at a time which contrasts with a CNN which takes in input a lot of pixels simultaneously(or in parallel). 

![t1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-27%2016-55-47.png)

So, Attention+CNN is the attention. Self Attention and Multi-Headed Attention are its two types.

![t2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-27%2017-01-16.png)


### Self Attention

Given a sentence, we will calculate Attention based vector representation for each word. Let's say we want to calculate this for the third word "l'Afrique" or "Africa". According to the context we will know whether it's an holiday destination or second largest continent or site of historical interests, etc. Depending upon how we are thinking of 'Africa', we choose to represent it differently, and that's what A^<3> will do. It will look at the sorrounding words to look at what's actually going on, and then find its appropriate representation.

![s1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2007-11-49.png)

We can think of these exponential terms as the attention values. For every word, we have q^<3>, k^<3>, V^<3>. 

![s2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2007-33-39.png)

q: Query, k: Key, V: Value

W^q, W^k, W^v are the parameters of learning algorithms. The inner product q^<3>* k^<3> is responsible for answering how good is 'visite' answer to the question to what;s going on in Africa, etc.

### Multi Head Attention
For loop over the self attention architecture. Self attention calculated for each word is called 'head'.
W1q, W1k, W1V are learned parameters that answers the question: 'What's happeneing there?'

For multi head, we ask multiple questions, each responsible for answering the most likely word. And then they are stacked. In reality, these values of heads are calculated parallely because of no inter-dependence.

![m1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2007-56-00.png)

### Transformers Network

![n1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2008-15-37.png)

![n2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2008-15-21.png)

![n3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-06-28%2008-15-06.png)
