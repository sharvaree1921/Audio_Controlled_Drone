## Week 2: Natural Language Processing and Word Embeddings

### Word Representation

So far, we represent words as vocabulory of words. Vocabulory could be 10,000 words long and each word in it is represented using one-hot encoding. One disadvantage of this is that each word is a thing in itself and it does'nt allow the algorithms to generalize the cross words.
Note that, the inner product of any two one-hot encoded vectors is zero. So, let's take an example: 

I want an Orange _______.

I want an Apple ________.

![wr1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-34-57.png)

The most likely word for the first and second blank space is 'juice'.
Even though the learning algorithm has learned the sentence that I want an Orange _juice_. Then the relationship between orange and apple is not as closer to any of the other words. Hence, the learning algorithm finds it difficult to recognize apple _juice_ is also as popular as orange _juice_. 

So, instead of one-hot representation, we can instead learn 'Featurized representation'. So, something like this:

![wr2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-41-37.png)

Let's say we take 300 features. Hence, e_5931 is 300 dimensional vector for the 'Man'. See the above figure. You can see that the probabilities/ numbers assigned with orange and apple are almost similar in most of the cases. Hence, this increases the probability of _juice_ being in the blank space for both of the sentences.

**Visualizing Word Embeddings:**
The representation that uses some sort of feauturized represntations in maybe a 300 dimensional space, these are called embeddings. For ex. the word 'Orange' is represnted as point in 300-dimensional space and hence is embedded in that space.The word 'Apple' is embedded to some other point in the same space. These features are visualized by mapping into much lower dimensional space. We can actually plot a 2D data and look at it. Word embeddings has been one of the most important ideas in NLP, in Natural Language Processing. 

![wr3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-56-01.png)

