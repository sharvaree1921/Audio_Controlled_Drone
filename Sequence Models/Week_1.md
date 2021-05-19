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

Also, each training example is denoted by x^{<i>}. Hence, the t-th feature of the i-th training input is given by x^{<i><t>}. Similarly y^{<i><t>}.
Similarly, T_x^{i} and T_y^{i} are input and output lengths of the i-th training sample.
  
![]{}  
  
**How do we represent individual words of a sentence in NLP?**

Vocabulory. Given a dictionary size of say 10,000.(Usually it's 30,000/50,000)
Use one hot encoding for the dictionary array for representating each word in the given sentence. 
  
![]()
  

  
