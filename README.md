IMAGE CAPTIONING GENERATOR Deep Learning based CNN–LSTM Encoder–Decoder
Architecture

------------------------------------------------------------------------

PROJECT OVERVIEW This project implements an end-to-end Image Captioning
System that automatically generates meaningful textual descriptions for
input images using deep learning.

It combines: - Computer Vision (CNN – VGG16) - Natural Language
Processing (LSTM) - Encoder–Decoder Architecture

------------------------------------------------------------------------

PROBLEM STATEMENT Given an input image, the model generates a meaningful
caption.

Unlike: - Image classification - Object detection

This system performs full sentence generation.

Example: Input Image: Dog playing in park Output: “A brown dog is
playing with a ball in the grass.”

------------------------------------------------------------------------

ARCHITECTURE OVERVIEW

1)  ENCODER – VGG16

-   Pretrained VGG16 (ImageNet)
-   Removed final classification layer
-   Extracted 4096-dimensional feature vector
-   Used transfer learning

Each image is converted into a fixed 4096-dimension feature vector.

2)  DECODER – LSTM

-   Embedding Layer
-   LSTM (256 units)
-   Dense Softmax Layer

The LSTM predicts the next word based on: - Image features - Previously
generated words

------------------------------------------------------------------------

DATASET - Image-caption dataset (Flickr8k type structure) - Each image
has multiple captions - Images stored separately - Captions stored in
text file

Structure: image_name.jpg → 5 captions

------------------------------------------------------------------------

DATA PREPROCESSING

1)  Text Cleaning

-   Convert to lowercase
-   Remove punctuation
-   Remove short words

2)  Added Special Tokens startseq endseq

Example: startseq a dog is running endseq

3)  Tokenization

-   Words converted to integers
-   Created word-to-index dictionary

4)  Padding

-   Fixed-length sequences
-   Used pad_sequences

------------------------------------------------------------------------

CUSTOM DATA GENERATOR

To handle memory efficiently: - Implemented custom generator - Avoided
loading entire dataset into RAM

For each image and caption: Input: - Image features - Partial text
sequence

Output: - Next word (one-hot encoded)

Example: Input: Image vector + “startseq a dog” Output: “is”

This technique is called Teacher Forcing.

------------------------------------------------------------------------

MODEL TRAINING - Loss: Categorical Crossentropy - Optimizer: Adam -
Epochs: 60+ - Batch Size: 64

The model minimizes error between predicted word and actual next word.

------------------------------------------------------------------------

CAPTION GENERATION (INFERENCE)

Steps: 1. Extract image features using VGG16 2. Start with “startseq” 3.
Predict next word 4. Append word 5. Repeat until “endseq”

Used Top-K Sampling (k=5) to generate more natural captions.

------------------------------------------------------------------------

EVALUATION Used BLEU Score: - BLEU-1 - BLEU-2

BLEU score measures similarity between generated caption and reference
captions.

------------------------------------------------------------------------

CHALLENGES FACED - Overfitting - Long training time - Memory
constraints - Repetitive captions - Large vocabulary size

Solutions: - Dropout - Custom data generator - Top-K sampling -
Vocabulary threshold reduction

------------------------------------------------------------------------

WHY LSTM OVER GRU? - LSTM handles long-term dependencies better - GRU is
faster but less expressive

------------------------------------------------------------------------

FUTURE IMPROVEMENTS - Add Attention Mechanism - Use Beam Search - Use
Transformer models (ViT + GPT)

------------------------------------------------------------------------
 SUMMARY :-This project combines computer vision and NLP using a
CNN-LSTM encoder-decoder architecture. VGG16 extracts image features,
LSTM generates captions word-by-word, and BLEU score evaluates
performance.
