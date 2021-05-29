# Sequence Models and Attention Mechanisms

## Various Sequence to Sequence architectures

### Basic Models

**Sequence to Sequence Model:** x^1 to x^5 are inputs(french words) and y^1 to y^5 are outputs(translated words) for the given example.
Let's take an encoder network. It can be a GRU or LSTM network feeding with the input french words. A decoder network takes input as the output of the encoder network and it outputs the translated network.

One of the most remarkable recent results
in deep learning is that this model works.
Given enough pairs of French and English sentences,
if you train a model to input
a French sentence and
output the corresponding English translation,
this will actually work decently well.
This model simply uses an encoding network whose job it
is to find an encoding of the input French sentence,
and then use a decoding network to then
generate the corresponding English translation. 

![sm1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2006-17-38.png)

Image Captioning uses something similar concept: Given input image, it is fed into a pre-trained Alex-Net Architecture which can give you 4096-dimensional feature vector. The pre-trained network can be encoded network of an image. We can then take this and feed it to an RNN whose job it is to generate the caption one word at a time. Similar to what we saw with machine translation, translating from French the English, you can now input a feature vector describing the inputs and then have it generate an output set of words, one word at a time. 

![sm2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2006-20-48.png)

### Picking the most likely sentence

**Machine Translation as building a conditional language model**
Language model allows us to estimate the probability of a sentence. Note that the decoder model of Machine Translation is pretty much similar to the Language model. So, instead of input zero vector to Language model, we now have the encoded feature vector. Thus, we are not computing the probability alone but we are computing conditional probability.

![pc1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2006-39-08.png)

For actually translating the sentence: Sampling the distribution randomly won't help here in order to find the most likely translation. However, we find the English sentence that maximizes that conditional probability. The most common algorithm to do so is the _Beam Search_ algorithm.

Why not _Greedy Search_? In this algorithm, given the first word, we choose the word which is most likely. Given the secind word, we choose the word which is most likely, ... and so on. 

![pc2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2006-49-58.png)

The no. of words in English Vocabolury is so so large, that predicting the next word given some prior words is really difficult. For a 10 word long sentence and 10,000 words dictionary, we have 10000^10 choices which is exponentially very very large. Hence, we use something sort of 'Approximate Algorithm' which finds the sentence with maximum conditional probability.

### Beam Search

In this Beam Search Algorithm, first we have the input French words. We also have a beam serach algorithm paramter called as **Beam Width**: *b*. When b=3(say), it will find 3 most likely words from the given vocabulory of say 10000 words. If b=10, it will find 10 such words. The beam width indicates the most likely(rather most probable) choices for the first word. 
So, to be clear in order to perform this first step of Beam search,
what you need to do is run the input French sentence through
this encoder network and then this first step will then decode the network,
this is a softmax output overall 10,000 possibilities.
Then you would take those 10,000 possible
outputs and keep in memory which were the top three. 

![bs1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2007-07-35.png)

For figuring out that, what the second word is: 

![bs2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2007-17-01.png)

For figuring out that, what the third word is: 

![bs3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2007-20-59.png)

### Refinements to Beam Search

**Length Normalization** can help us get much more better results in the Beam Search Algorithm.
The Beam Search algorithm is nothing but as shown in the image below. The product of probabilities may result in Numerical Underflow as all the probabilities are less than 1. Taking log will result i its addition and hece give more stable result. 

Another issue with this objective function is that when the length of the sentence is big, the product of probabilities is much lower and hence the probability of the sentence is low.and may give undesirable results. 

Hence, the objective function tends to prefer the shorter length sentences. Normalizing/Averaging significantly reduces the penalty for outputing the longer translations. 

![r1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2007-56-04.png)

Larger the B is, larger the possibilities, more heavy is the computation.

![r2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2008-00-38.png)

### Error Analysis in Beam Search

![e1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2008-14-21.png)

![e2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2008-17-24.png)

![e3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2008-19-52.png)

If you find that beam search is responsible for a lot of errors,
then maybe is we're working hard to increase the beam width.
Whereas in contrast, if you find that the RNN model is at fault,
then you could do a deeper layer of analysis to try to figure out if you want
to add regularization, or get more training data, or
try a different network architecture, or something else

### Bleu Score

[See Coursera Video](https://www.coursera.org/learn/nlp-sequence-models/lecture/kC2HD/bleu-score-optional)

### Attention Model Intuition

Until now, we were using two different models for input and output of the words. The Attention model architecture simplifies this all.
![see the video](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2009-01-02.png)

We are using simple bidirectional RNN.

What the Attention Model would be computing is a set of
attention weights and we're going to use Alpha one, one
to denote when you're generating the first words,
how much should you be paying attention to this first piece of information here.
And then we'll also come up with a second that's called Attention Weight,
Alpha one, two which tells us what we're trying to compute the first work of Jane,
how much attention we're
paying to this second work from the inputs and so on and the Alpha one, three and so on,
and together this will tell us what is
exactly the context from denoter C that we should be paying attention to,
and that is input to this R and N unit to then try to generate the first words

### Attention Model

t' for french words.

[see thr video](https://www.coursera.org/learn/nlp-sequence-models/lecture/lSwVa/attention-model)

![am1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2009-25-22.png)

![am2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2009-37-33.png)

![am3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-29%2009-39-01.png)





