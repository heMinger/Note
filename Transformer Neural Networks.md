[Transformer Neural Networks, ChatGPT's foundation, Clearly Explained!!!](https://www.youtube.com/watch?v=zxQyTK8quyY&t=167s)
# data: 6/11
writer: lmh \

focus on how a Transformer neural network can translate a simple English sentence into spanish.

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
