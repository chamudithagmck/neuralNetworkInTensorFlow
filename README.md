# **TensorFlow 2 This repository contains a simple, beginner-friendly introduction to building machine learning models using TensorFlow 2 and the Keras API.**

## **Overview**

This project serves as a quickstart guide demonstrating how to:

* Load and prepare a prebuilt image dataset.  
* Build a sequential neural network to classify images.  
* Train the neural network.  
* Evaluate the accuracy of the trained model.

## **Dataset**

The model uses the **MNIST dataset**, a standard computer vision dataset containing grayscale images of handwritten digits.

* The raw pixel values of the images range from 0 through 255\.  
* During the data preparation phase, these values are scaled to a range of 0 to 1 by dividing them by 255.0. This also converts the sample data from integers to floating-point numbers.

## **Model Architecture**

The image classifier is built using tf.keras.models.Sequential and consists of the following stacked layers:

1. **Flatten**: Flattens the input format from a 28x28 pixel 2D array into a 1D array.  
2. **Dense**: A fully connected neural layer with 128 nodes using a relu activation function.  
3. **Dropout**: Randomly drops 20% of the input units at each update during training to help prevent overfitting.  
4. **Dense (Output Layer)**: A final fully connected layer with 10 nodes (representing the digits 0-9). For each example, this layer returns a vector of logits (log-odds scores).

## **Training and Evaluation**

Before training, the model is compiled with the following configurations:

* **Loss Function**: SparseCategoricalCrossentropy (set to accept logits directly).  
* **Optimizer**: adam  
* **Metrics**: accuracy

The model is trained using the Model.fit method for **5 epochs**. Upon evaluation using the Model.evaluate method against the test set, the classifier achieves an accuracy of approximately **98%**.

## **Generating Probabilities**

By default, the final layer outputs logits. If you want the model to return easily interpretable probabilities (where the scores for all classes sum to 1), you can wrap the trained model and attach a softmax layer to it:

Python  
probability\_model \= tf.keras.Sequential(\[  
  model,  
  tf.keras.layers.Softmax()  
\])  
