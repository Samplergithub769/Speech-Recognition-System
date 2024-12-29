# Speech-to-Text with LJSpeech Dataset

Speech recognition is an interdisciplinary subfield of computer science and computational linguistics that develops methodologies and technologies that enable the recognition and translation of spoken language into text by computers. It is also known as automatic speech recognition (ASR), computer speech recognition or speech to text (STT).

This project demonstrates a speech-to-text model trained using the LJSpeech dataset. The goal of the project is to convert spoken language into written text using deep learning techniques. The LJSpeech dataset, The dataset contains 13,100 audio files as wav files in the /wavs/ folder. The label (transcript) for each audio file is a string given in the metadata.csv file.The fields are:
- ID: this is the name of the corresponding .wav file
- Transcription: words spoken by the reader (UTF-8)
- Normalized transcription: transcription with numbers, ordinals, and monetary units expanded into full words (UTF-8).
  
Each audio file is a single-channel 16-bit PCM WAV with a sample rate of 22,050 Hz.

# Steps required to build Speech-to-text model
1. Install Dependencies
- pandas: A powerful library for data manipulation and analysis. It is used to load and process data efficiently.
- numpy: A fundamental package for scientific computing in Python. It is used for working with arrays and performing mathematical operations.
- tensorflow: A popular open-source machine learning library. We use it to define, train, and evaluate our neural network models.
- keras: A high-level API for building and training deep learning models within TensorFlow.
- matplotlib: A plotting library used for creating static, animated, and interactive visualizations in Python. We use it to visualize model training metrics like loss and accuracy.
- IPython: Provides interactive computing features. The display module is used to display visual outputs, like training progress.
- jiwer: A library to evaluate speech recognition models by calculating the Word Error Rate (WER), which is commonly used for evaluating speech-to-text models.
  
2. Load the LJSpeech Dataset
- Keras is used to download and extract the LJSpeech dataset
   
4. Data Preprocessing
  
   We preprocess the dataset in the following steps:
- Load the metadata: We read the metadata file that contains the names of the audio files and their corresponding transcriptions.
- Split the data into training and validation sets (90% training, 10% validation).
- Define a character set: We define the set of characters (letters, punctuation, and spaces) that the model will recognize.
- Preprocess audio data: Convert the audio into spectrograms using the Short-Time Fourier Transform (STFT). Normalize the spectrograms to make the model more stable.
- Preprocess text data: Convert text to lower case and map each character to an integer index.
  
4. Model Architecture

   We define a model similar to DeepSpeech2:
- Convolutional Layers (CNN): To extract features from the spectrograms.
- Recurrent Layers (RNN): To process sequential data, specifically GRU cells.
- Fully Connected Layer: To produce predictions for each time step in the sequence.
- CTC Loss: The Connectionist Temporal Classification (CTC) loss is used to handle sequences of varying lengths
  Model Overview:
- Conv2D Layers: Extract features from the spectrogram.
- Bidirectional GRU Layers: Capture sequential dependencies in the audio data.
- Dense Layer: For final classification.
- Softmax Output Layer: Produces the predicted transcription.
  
5. Training the Model
- Define the model with the appropriate input and output dimensions.
- Compile the model using the Adam optimizer and the custom CTC loss function.
- Train the model using the training dataset, and validate it on the validation dataset.
- Monitor performance using a custom callback that evaluates Word Error Rate (WER) after each epoch.
  
6. Evaluation
  
   After training, we evaluate the model on the validation set:
- We use the Word Error Rate (WER) to measure the model's accuracy.
- The model is tested with random samples from the validation set to see how well it transcribes spoken text.
  
7. Inference
  
   After training, the model can be used for inference:
- Input a new audio file, process it through the model, and get the transcription.
- The model's predictions are decoded and compared to the target transcription.

Conclusion
- In practice, train for around 50 epochs or more. Each epoch takes approximately 5-6mn using a GeForce RTX 2080 Ti GPU. The model we trained at 50 epochs has a 
  Word Error Rate (WER) ≈ 16% to 17%.

Some of the transcriptions around epoch 50:

![image](https://github.com/user-attachments/assets/acbc30b0-f042-4b0d-b924-1999d531c13d)

![image](https://github.com/user-attachments/assets/9a0a30f1-fde2-4d71-b95e-fcb4c8350acd)



