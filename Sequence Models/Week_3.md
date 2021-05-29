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


