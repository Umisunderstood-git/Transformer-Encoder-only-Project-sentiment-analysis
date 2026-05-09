This is info file to understand the code, logic and the concepts used in int the encoder only code

-> About project
What is it about?
The code is about training a transformer with the sequence data to learn if the sentence is positive or negative

->How does the training data look like?

sentence  | label
The labels are 1 implying positive sentiment and 0 implying negative sentiment

->High level steps:

1) Tokenization
2) Input sentence data tokenization & embedding
3) Literal position number tensor vector - [0,1,2,3,4,5,6,7] and then embedding of this
4) Positional embdeddings= token_embeddings + embeded_positions
5) Making a imaginary matrix for transformer
6) Passing this to multihead attention layer
7) Passing it to addition for residual addition
8) Passig it through the normalization step
9) Declaring a feed forward neural network (to just add non linearity)
10) Passing it to addition for residual addition
11) Passig it through the normalization step and dropout
12) Passing it through global average pooling 1D
13) Declaring a classification head for sentiment analysis  (2 layers- 1  forward pass using relu and other one is sigmoid for binary classification)
14) Compiling the model by showing it how  the input layer looks now and the original one
15) Training the model with the position embeded matrix
16) Testing the data by creating a sentence getting it tokenized & embeded using the same embed object
17) Writing the if else for sigmoid in terms of displaying the output




Understanding each step in depth

1) Tokenization:
   Here we have 24 sentences. By going through the data I saw that the sentence with most words is not more than 5.
   AI/ML book recommends that we take at least 30 percent of the longest sentence as our maximum length, so we considered sequence_length=8

   
