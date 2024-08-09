# POEM GENERATOR
## 1. Introduction
In this project, we will implement a program using a Text Generation model with the theme of generating Vietnamese pentasyllabic poetry (5-word verse) based on an input line provided by the user. Therefore, the Input/Output of the program is as follows:
- Input: A string consisting of 5 words (representing the first line of the poem).
- Output: n subsequent lines of the poem (n is adjustable)
- 
With the poetry generation model, we will build it using a transformer model (utilizing both the encoder and decoder components).
Transformer architecture:

![image](https://github.com/user-attachments/assets/b2995154-06f2-44ea-b786-f294dc8e9382)

## 2. Dataset
### 2.1. Collect data
For poetry data, there are many websites that compile Vietnamese and international poetry. However, in this project, we will collect pentasyllabic poems from the website [thivien.net](https://www.thivien.net/), a large site dedicated to compiling various genres of Vietnamese poetry

![image](https://github.com/user-attachments/assets/6474b0c7-f968-4e2f-9a81-f87a79d2fdde)

### 2.2. Prepare data
After completing the collection of a certain amount of data, we proceed to process the collected dataset to align with the Input/Output requirements of the transformer model

![image](https://github.com/user-attachments/assets/b4fd33b8-428a-472b-a292-969e2e74260c)

This is the computational flow of the transformer model. The Input Embedding is the Embedding Vector of the input line of poetry. The Output Embedding is a shifted version of the corresponding labeled line of poetry.
Similar to other text-related tasks, we will also perform data normalization. The main techniques applied here include lowercasing, stripping, and punctuation removal. Additionally, the input data for the transformer model requires two tokens, <start> and <end>, to be added at the beginning and end of each data point. Therefore, we will also handle this in the normalization function
- Identify the data X and y: First, we split the poem into two variables, X and y. Since the model will generate the next line of poetry from a given line. Thus, when iterating through a poem with n lines
- Tokenization: To feed the lines of poetry into the transformer model for training, we need to convert them into vectors where each word is represented by its index in the vocabulary (words not found in the vocabulary are encoded as <oov>)
- Padding: We need to ensure that the Input/Output vector sequences always have the same length. To achieve this, we use the pad_sequences() function

![image](https://github.com/user-attachments/assets/37af318e-d65c-4964-baf2-bb4b1463e2b7)

## 3. Build model
- Define PositionalEncoding layer

![image](https://github.com/user-attachments/assets/751f3bff-f42f-40a9-91d4-62be7844d6ec)

- Define Self-attention based layers: BaseAttention, CrossAttention, GlobalSelfAttention, CausalSelfAttention
- Define FeedForward Network Layer
- Define Transformer Encoder Block:

![image](https://github.com/user-attachments/assets/d6d35f5e-b0f6-4cec-92f5-4ead106b7337)

- Define Transformer Decoder Block:

![image](https://github.com/user-attachments/assets/0042d7e4-ef19-44a5-9f56-261ea8bdff15)

- Define Transformer Model
- Declare transformer model: Initialize the model along with some hyperparameters
  + N_LAYERS: number of transformer encoder-decoder block
  + D_MODEL: embedding dims of token is performed in transformer
  + D_FF: number of nodes in hidden layer of Feedforward Network layer
  + N_HEADS: number of head in multi-head attention layers
  + DROPOUT_RATE: the dropout rate in the Dropout() layers within the transformer
  + VOCAB_SIZE: size of vocabulary

## 4. Training and evaluate

![image](https://github.com/user-attachments/assets/673a7165-dd1b-414a-ac19-ffd980ff50bf)

![image](https://github.com/user-attachments/assets/65896ce3-a86c-4922-942f-cb6f9d0718fa)

## 5. Results 

![image](https://github.com/user-attachments/assets/d6cd8672-366d-4436-adc0-dd8b19b48a8b)

![image](https://github.com/user-attachments/assets/dca87c2c-0cd6-47c2-8c56-824578ecb5bb)



