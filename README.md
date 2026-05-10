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

Use of layers.TextVectorization(): This allows us to form a object that we can use to adapt on our dataset
here the parameter max_tokens is the number of unique tokens the data will have. I have taken 1000 here to be safe. Flow of this object -> it tokenizes the unique word, but if number of unique tokens go beyond the max_tokens then it throws a error


2) Input sentence tokenization and embedding
   we embed the data tokens using layers.Embedding
   , we chose input dimension 1000 because of the same reason. Its the maximum unique tokens it will see       in the data set. We gave output_dim =16, this means that output of each token should be a 16 dimension     vector. eg 4 -> [0.1,0.2,0.7,0.6..........0.7], len(4)=16. Understand the shape of the data after embedding

   Shape of the data before embedding: 24 sentences (batch size=24)
   maximum word length in a sentence=8
   so our data after tokenization looks like 24,8
   after embedding each token expands into a 16 dimension vector, so for 1 word there is a 16 dimension vector, so 24 is the batch size, 8 words in a single sentence and 16 dimensional vector for each word, sp data looks like (24,8,16).
Here (1,8,16) will be first sentence, (2,8,16) will be second sentence.  
   

4) Literal position number tensors:
   forming a literal tensor with position numbers, why? we will take embeds of this to add with our token numbers
   here since there are max 8 positions, so we will just be taking input_dim=8. 
   Since our goal is to directly add the this positional embeds to our token embeds, we would want the shape similar to token embeds. 1 sentence token embed shape again is (1,8,16), so we give input_dim=8 and output_dim=16 for our positional embeds and thus our positional embeds output shape becomes (1,8,16)


Positional embdeddings= token_embeddings + embeded_positions

Adding the positional embeds token embeds makes a transformer model understand the position of each word in the incoming sequence. Since transformer takes entire sequence for forward pass and doest see 1 word by other like RNN and LSTM we need to positionally embed it

   How does adding positional embeds and token embeds giving positional significance to each toke, because ultimately model is just going to see a 3d tensor for training? (Imp concept)
   Its because when we add positional vectors, we just slightly nudge the og token embeds,Transformer model in high dimensional space when word is repeated a lot many times, sees this vector and understands the og word and the added positional embeds inside it, and thus decide its attention.


   
