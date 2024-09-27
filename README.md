# Hungarian to English Language Translation Model

This project implements a sequence-to-sequence language translation model that translates sentences from Hungarian to English using Long Short-Term Memory (LSTM) networks. The model is trained on parallel datasets, where each Hungarian sentence has a corresponding English translation. 

## Project Overview

This project focuses on creating a machine translation model using LSTM networks to convert Hungarian sentences to English. The model takes a Hungarian sentence as input and outputs its English translation. Special tokens like `<sos>` (start of sentence) and `<eos>` (end of sentence) are used to help the model learn sentence structure and boundaries.

## Workflow

1. **Load Dataset**: Load a dataset containing parallel Hungarian-English sentence pairs.
2. **Split Dataset**: Separate the dataset into source (`x`) and target (`y`) language pairs.
3. **Preprocessing**:
   - Perform Unicode normalization.
   - Apply punctuation removal via regular expressions (regex).
4. **Target Tagging**: Add `<sos>` and `<eos>` tags to the target sentences.
5. **Tokenization**: 
   - Create tokenizers for the source (Hungarian) and target (English) sentences.
   - Convert the text into sequences of integer tokens.
6. **Padding Sequences**: Pad sequences to ensure uniform length.
7. **Model Training**: Train the LSTM model using the processed data.
8. **Inference**: Use the trained model to translate new Hungarian sentences into English.

## Model Architecture

### Key Components
- **Embedding Dimension**: 
  - Each word is represented as a 128-dimensional vector.
- **Hidden Units**: 
  - LSTM units have 256 hidden units, representing the capacity to capture dependencies in the sequence.
- **Batch Size**: 
  - The model processes 32 sequences at a time during training.

### Encoder
- **Function**: 
  - Processes the Hungarian sentence and encodes it into a fixed-size context vector.
- **Components**:
  - **Embedding Layer**:
    - Maps input sequence (word indices) into dense vectors of size `embedding_dim = 128`.
  - **LSTM Layer**:
    - Outputs both the sequence of LSTM outputs and the final hidden and cell states.
    - Responsible for capturing the context of the input sentence.

### Luong Attention Mechanism
- **Function**: 
  - Focuses on relevant parts of the encoder's output while decoding each token.
- **Operation**:
  - Computes attention scores between the current decoder output and encoder outputs.
  - Generates a context vector that influences the next token prediction.

### Decoder
- **Function**: 
  - Generates the English sentence, one word at a time, based on the context provided by the Encoder and the previous decoder state.
- **Components**:
  - **Attention Layer**:
    - Luong Attention mechanism computes a weighted context vector.
  - **LSTM Layer**:
    - Takes the previous word’s embedding, hidden state, and context vector as input.
    - Produces the next word’s logits.
  - **Dense Layer**:
    - Maps the LSTM output to the target vocabulary size to predict the next word.

## Results

- Sample translation:
  - **Input**: "Teszek rá, mit mondasz!"
  - **Output**: "I don't care what you say."