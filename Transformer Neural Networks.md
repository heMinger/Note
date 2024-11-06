[Transformer Neural Networks, ChatGPT's foundation, Clearly Explained!!!](https://www.youtube.com/watch?v=zxQyTK8quyY&t=167s)
# data: 6/11
writer: lmh

*focus on how a Transformer neural network can translate a simple English sentence into spanish.*

# Encoder

## word embedding: convert input and output words into numbers
*caz neural networks usually noly have numbers for input values*

- main idea: use a relatively simple neural network that has one input for every word and symbol in the vocabulary that you want to use.
![image](https://github.com/user-attachments/assets/806d2571-2687-4a03-8120-52adf056ecd3)
1. for each word, input of neural network is an vector of 1s and 0s. position of corresponding word is 1 and others are 0s.
2. neural networks for different words share weight, namely, we reuse the same word embedding network for each input or symbol.
3. weights in nn start out as random numbers, and optimized by bp in training time.

## Positional encoding: keep track of word order

1. in transformer, numbers that represent the word order come from a sequence of alternating Sine and Cosine squiggles.
- each squiggle gives a specific position values for each word's embeddings.
- 横坐标表示第几个单词，对应的纵坐标代表这个单词的position value
- ![image](https://github.com/user-attachments/assets/75a6dbd1-4b9e-4437-9500-6a9e35ba189c)

2. sum position values and embedding values
- ![image](https://github.com/user-attachments/assets/ffd84b21-d52c-4649-900b-6ae6a24dfec3)
- the bottom is result of word embedding
- the medium is poition values, color of boxes corresponds to the color of squiggles in the last picture.
- the top is sum of embedding values and position values, 
3. reverse the order of the input words: "squatch eats pizza" -> "pizza eats squatch"
 ![image](https://github.com/user-attachments/assets/25f4e024-f08d-4d2a-aa02-fffbd41517e4)

## Self-Attention: track the relationship among words
[more for Attention](https://www.youtube.com/watch?v=PSs6nxngL6k)
1. Query
- ![image](https://github.com/user-attachments/assets/cb81b1b0-fbad-402c-a60d-c8956cf0f8fb)
- multiply position encoded values by a pair of weights, and add those products together.
- representation of word: two(depends on specific circumstances) position encoded values -> two new values calles **Query**.
```diff
- why should we generate two new values to represent the word?
```
2. Keys
- ![image](https://github.com/user-attachments/assets/7cd8524f-342a-45af-8861-d908784957db)
- create two new values just like we did for the query, two new values called **Key**.
3. **similarity** between words:
- use dot product between Query and Key to represent the similarity between words.
- ![image](https://github.com/user-attachments/assets/f82a71d5-7fc8-4591-968a-6eedf6519cd6)
- we should calculate the similarity between one word to all words, for example, we should calculate similarities between Let's and Let's and Let's and go.
4. higher similarity -> more influence
- first run similarities course through soft max function
- softmax: preserve the order of the input values from low to high, and translates them into numbers between 0 and 1 that add up to 1.
- ![image](https://github.com/user-attachments/assets/264891d7-fa75-4f91-952f-2501352a6367)
- if we calcuated the similarities between word A with all words, the similarities indicate the infulence of all words for word A.
5. Values
- create two new values to represent words, and scale the values by the result of softmax function.
- sum the scaled values, if we calculated the similarites between word A with all words, the sum of all scaled words are the **Self-Attention value** for word A.
6. overall
![image](https://github.com/user-attachments/assets/f886f4cd-f253-4377-b6d2-ec54ec0e5a1c)
7. if we calculte the self-attention value of another word, we just need to calculate the corresponding query -> similarities -> softmax function -> sum of scaled values
8. notes:
- no matter how many words are input into the Transformer we just reuse the same sets of weights for Self-Attention Queries, Keys and Values.
- we can calculate the Queries, Keys and Values for each word at the same time -> high parallelism
9. the reason we build **two new values** to represent the word rather than just take the result of word embedding:
- self-attention values for each word contain input from all of the other words, and this helps give each word context and this can help establish how each word in the input is related to the others.
- we think of this unit with its weights for calculating queries keys and values as a self-attention cell -> we can create a stack of self-attention cells each with its own sets of weights to correctly establish how words are related in complicated sentences and paragraphs.
(1) weigths in self-attention cell could apply to the position encoded values for each word -> to capture different relationships among the words.
10. Residual Connections
- take the position encoded values and added them to the self-attention values.
- makes it easier to train complex neural networks, by allowing the self-attention layer to establish relationships among the input words without having to also preserve the word embedding and positioning coding information.
- ![image](https://github.com/user-attachments/assets/948cad3e-084e-4a84-b9cb-ceba612cdbbf)

## features of Transformer 
![image](https://github.com/user-attachments/assets/d28fc0e9-1feb-4f10-8ce9-706f38301ce0)
1. word embedding: encode words into numbers
2. positional encoding: encode the positions of the words
3. self-attention: encode the relationship among the words
4. residual connections: relatively easily and quickly train in parallel.

# Decoder

1. same processes like encoder, start with <EOS>

## Encoder-Decoder Attention
**allow Decoder to keep track of the significant words in the input.**
1. we create two new values to represent the query for the EOS token in the decoder
- new Query! take the sum of self-attention values and position encoded values as input
- ![image](https://github.com/user-attachments/assets/4d06e5a2-2bb2-4a1d-b03f-83208429b2c8)
2. create keys for each word in the encoder
- new Key! take the sum of self-attention values and position encoded values as input
- ![image](https://github.com/user-attachments/assets/b3b324cd-a916-4555-85bc-41963dce0b6e)
3. calculate similarities between the EOS token in the decoder and each words in the encoder
- cause we want to find the influnce(significance) of words in encoder with current word(EOS token) in decoder.
- calculate similarities by dot product
- then run similarities through a softmax function
- ![image](https://github.com/user-attachments/assets/53dcca1c-87c4-4c76-8da1-3f7471a41fce)
- then we get the percentage of each input word to use when Decoder determines what should be the first tanslates word.
4. then we calculate Value for each input word
- and scale those Values by the SoftMax percentages
- and then add the pairs of scaled values together to get the Encoder-Decoder Attention values.
- ![image](https://github.com/user-attachments/assets/a48b9b60-90a7-44a5-b368-143fc9046835)
5. Residual Connections
- allow Encoder-Decoder Attention to focus on relationships between the output words and the input, without having to preserve the Self-Attention or Word and Position Encoding that happened earlier.
- ![image](https://github.com/user-attachments/assets/f0ad0c80-7b4e-428e-9bb4-4f9ae1ec698d)

6. Fully Connected Network
- take these two values that represent the EOS token in the decoder and select one from vocabulary.
- FCN got four values(in this case, we have "ir", "vamos", "y", "<EOS>"),
- and run softmax function to select first output word.
- ![image](https://github.com/user-attachments/assets/b3be2f0b-dbf4-4799-8e6f-91c5f458ea63)

7. circul
- when we get the first output word, take it as input and loop.
- decoder stops when outputs an EOS token.

#### Notes
  1. attention could be stacked: no matter where it be used, self-attention or encoder-decoder attention
  2. weight in same attention shared for all words, but different attention got different set of weights.

