# 🧠 Deep Learning Sentiment Analysis (LSTM)

## 🔬 Research Overview
While traditional machine learning models (like Naive Bayes) treat words as isolated units, human language relies heavily on context. This project implements a **Long Short-Term Memory (LSTM)** neural network to perform sentiment classification on complex customer feedback.

Unlike standard models, this architecture utilizes **Word Embeddings** to understand semantic relationships (e.g., understanding that "delayed" and "late" are related concepts).

## 🛠️ Model Architecture
* **Framework:** TensorFlow / Keras
* **Embedding Layer:** Word2Vec (Pre-trained embeddings to capture semantic meaning).
* **Deep Layers:** * `LSTM` (128 units) for sequence processing.
    * `Dropout` (0.5) to prevent overfitting.
    * `Dense` (Softmax) for final classification.
* **Optimization:** Adam Optimizer with Categorical Crossentropy loss.

## 📊 Performance
* **Training Accuracy:** ~90%
* **Validation Accuracy:** ~82%
* **Key Finding:** The LSTM model significantly outperformed baseline models in detecting sarcasm and indirect complaints, proving the value of deep learning for nuanced text data.

## 🚀 Usage
1.  Ensure `TensorFlow` and `Keras` are installed (`pip install tensorflow`).
2.  Load the dataset (CSV).
3.  Run the notebook to train the model over 10-20 epochs.
4.  Monitor the "Loss vs Accuracy" graphs generated in the final cells.
