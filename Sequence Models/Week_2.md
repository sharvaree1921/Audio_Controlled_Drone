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


### Using Word Embeddings

In this video, you see how we can take these representations and plug them into NLP applications. Continuing with the named entity recognition example,
if you're trying to detect people's names. Given a sentence like Sally Johnson is an orange farmer, hopefully, you'll figure out that Sally Johnson is a person's name, hence, the outputs 1 like that. if you can now use the featurized representations, the embedding vectors that we talked about in the last discussion.
Then after having trained a model that uses word embeddings as the inputs, if you now see a new input, Robert Lin is an apple farmer.
Knowing that orange and apple are very similar will make it easier for your learning algorithm to generalize to figure out that Robert Lin is also a human.

!we1[](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-22-50.png)

A durian is a rare type of fruit, popular in Singapore and a few other countries.
But if you have a small label training set for the named entity recognition task,
you might not even have seen the word durian or
seen the word cultivator in your training set.
I guess technically, this should be a durian cultivator.
But if you have learned a word embedding that tells you that durian is a fruit,
so it's like an orange, and a cultivator, someone that cultivates is like a farmer,
then you might still be generalize from having seen an orange farmer in your
training set to knowing that a durian cultivator is also probably a person.
So one of the reasons that word embeddings will be able to do this is
the algorithms to learning word embeddings can examine very large text corpuses,
maybe found off the Internet.
So you can examine very large data sets, maybe a billion words,
maybe even up to 100 billion words would be quite reasonable.
So very large training sets of just unlabeled text. 

Now having discovered that orange and
durian are both fruits by reading massive amounts of Internet text,
what you can do is then take this word embedding and apply it to your named
entity recognition task, for which you might have a much smaller training set,
maybe just 100,000 words in your training set, or even much smaller. 

This allows us to use **Transfer Learning**  
where you take information you've learned from
huge amounts of unlabeled text that you can suck down essentially for
free off the Internet to figure out that orange, apple, and durian are fruits. 

![we2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-24-58.png)

![we3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-36-55.png)

![we4](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-38-02.png)











