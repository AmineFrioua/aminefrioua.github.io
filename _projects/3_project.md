---
layout: page
title: Creating my own Neural Network
description: playing with matrix for fun
img: assets/img/4.jpg
importance: 3
category: fun
---

# Building a Neural Network from Scratch
As someone interested in machine learning and artificial intelligence, I've always been fascinated by the inner workings of neural networks. While there are plenty of pre-built models and frameworks available, I wanted to take on the challenge of building a neural network from scratch, both as a fun coding project and to deepen my understanding of the underlying theory.

## The Basics of Neural Networks
Before diving into the coding, let's review some of the basics of neural networks. At a high level, a neural network is a computational model inspired by the structure and function of the human brain. It's made up of individual neurons that are connected in layers, with each layer processing information and passing it on to the next.

The first layer, called the input layer, takes in the raw data. The output layer produces the final predictions or classifications, and the layers in between are known as hidden layers. Each neuron in the network takes in a set of input values, multiplies them by a set of weights, adds a bias term, and passes the result through an activation function. The activation function determines whether the neuron "fires" or not based on the input, weights, and bias.

During training, the network adjusts the weights and biases of the neurons in order to minimize the difference between the predicted outputs and the actual outputs. This process is known as backpropagation, and it involves computing the gradient of the loss function with respect to the weights and biases, and then updating them in the direction of the gradient.

## Building the Network
Now that we have a basic understanding of neural networks, let's start building our own. For this project, I'll be using Python and the NumPy library for numerical computing.

First, we'll define a class for our neural network. Our network will take in a set of input values, process them through a set of hidden layers, and produce a set of output values. We'll start by defining the basic structure of the network, including the number of input and output nodes, the number of hidden layers, and the number of neurons in each layer.

{% raw %}
```py
import numpy as np

class NeuralNetwork:
    def __init__(self, input_nodes, hidden_nodes, output_nodes, learning_rate):
        self.input_nodes = input_nodes
        self.hidden_nodes = hidden_nodes
        self.output_nodes = output_nodes
        self.learning_rate = learning_rate
        
        self.weights_input_hidden = np.random.normal(0.0, self.hidden_nodes**-0.5, 
                                                     (self.hidden_nodes, self.input_nodes))
        self.weights_hidden_output = np.random.normal(0.0, self.output_nodes**-0.5, 
                                                      (self.output_nodes, self.hidden_nodes))
        
        self.sigmoid = lambda x: 1 / (1 + np.exp(-x))


```
{% endraw %}

In the __init__ method, we initialize the input, hidden, and output nodes, as well as the learning rate. We also randomly initialize the weights between the input layer and the first hidden layer, and between the last hidden layer and the output layer.

We define the sigmoid activation function as a lambda function, since we'll be using it multiple times in the network.

Next, we'll define the train method, which will take in a set of input values and target values, and update the weights and biases of the network using backpropagation.

{% raw %}
```py
def train(self, inputs_list, targets_list):
    inputs = np.array(inputs_list, ndmin=2).T
    targets = np.array(targets_list, ndmin=2).T
    
    hidden_inputs = np.dot(self.weights_input_hidden, inputs)
        hidden_outputs = self.sigmoid(hidden_inputs)
    
    final_inputs = np.dot(self.weights_hidden_output, hidden_outputs)
    final_outputs = self.sigmoid(final_inputs)
    
    output_errors = targets - final_outputs
    hidden_errors = np.dot(self.weights_hidden_output.T, output_errors)
    
    self.weights_hidden_output += self.learning_rate * np.dot((output_errors * final_outputs * (1 - final_outputs)),
                                                              np.transpose(hidden_outputs))
    self.weights_input_hidden += self.learning_rate * np.dot((hidden_errors * hidden_outputs * (1 - hidden_outputs)),
                                                             np.transpose(inputs))


```
{% endraw %}

In the train method, we start by converting the input and target values into NumPy arrays. We then perform forward propagation, computing the outputs of the hidden and output layers. We calculate the errors at each layer by comparing the target values with the actual outputs.

Next, we update the weights and biases using backpropagation. We compute the gradient of the loss function with respect to the weights between the hidden and output layers, and between the input and hidden layers. Finally, we update the weights by multiplying the gradients with the learning rate and the corresponding layer outputs.

To make predictions with our neural network, we'll define the predict method:

{% raw %}
```py
def predict(self, inputs_list):
    inputs = np.array(inputs_list, ndmin=2).T
    
    hidden_inputs = np.dot(self.weights_input_hidden, inputs)
    hidden_outputs = self.sigmoid(hidden_inputs)
    
    final_inputs = np.dot(self.weights_hidden_output, hidden_outputs)
    final_outputs = self.sigmoid(final_inputs)
    
    return final_outputs
```
{% endraw %}

In the predict method, we perform forward propagation to compute the final outputs of the network based on the given input values. We return the final outputs as our predictions.

## Testing the Neural Network
Now that we've defined our neural network class, let's test it on a simple problem. We'll create a neural network that can predict whether a given person is male or female based on their height, weight, and age.

{% raw %}
```py
# Create a neural network with 3 input nodes, 2 hidden nodes, and 1 output node
network = NeuralNetwork(3, 2, 1, 0.1)

# Train the network using a set of example inputs and targets
training_inputs = [[170, 70, 25], [160, 55, 30], [180, 90, 40], [150, 45, 20]]
training_targets = [[1], [0], [1], [0]]

for i in range(1000):
    for inputs, targets in zip(training_inputs, training_targets):
        network.train(inputs, targets)

# Test the network by making predictions on new inputs
test_inputs = [[175, 75, 27], [165, 60, 35], [185, 95, 42]]
for inputs in test_inputs:
    prediction = network.predict(inputs)
    print("Prediction:", prediction)
```
{% endraw %}


Certainly! Here's the continuation of the blog post:

python
Copy code
    hidden_outputs = self.sigmoid(hidden_inputs)
    
    final_inputs = np.dot(self.weights_hidden_output, hidden_outputs)
    final_outputs = self.sigmoid(final_inputs)
    
    output_errors = targets - final_outputs
    hidden_errors = np.dot(self.weights_hidden_output.T, output_errors)
    
    self.weights_hidden_output += self.learning_rate * np.dot((output_errors * final_outputs * (1 - final_outputs)),
                                                              np.transpose(hidden_outputs))
    self.weights_input_hidden += self.learning_rate * np.dot((hidden_errors * hidden_outputs * (1 - hidden_outputs)),
                                                             np.transpose(inputs))
In the train method, we start by converting the input and target values into NumPy arrays. We then perform forward propagation, computing the outputs of the hidden and output layers. We calculate the errors at each layer by comparing the target values with the actual outputs.

Next, we update the weights and biases using backpropagation. We compute the gradient of the loss function with respect to the weights between the hidden and output layers, and between the input and hidden layers. Finally, we update the weights by multiplying the gradients with the learning rate and the corresponding layer outputs.

To make predictions with our neural network, we'll define the predict method:

python
Copy code
def predict(self, inputs_list):
    inputs = np.array(inputs_list, ndmin=2).T
    
    hidden_inputs = np.dot(self.weights_input_hidden, inputs)
    hidden_outputs = self.sigmoid(hidden_inputs)
    
    final_inputs = np.dot(self.weights_hidden_output, hidden_outputs)
    final_outputs = self.sigmoid(final_inputs)
    
    return final_outputs
In the predict method, we perform forward propagation to compute the final outputs of the network based on the given input values. We return the final outputs as our predictions.

Testing the Neural Network
Now that we've defined our neural network class, let's test it on a simple problem. We'll create a neural network that can predict whether a given person is male or female based on their height, weight, and age.

python
Copy code
# Create a neural network with 3 input nodes, 2 hidden nodes, and 1 output node
network = NeuralNetwork(3, 2, 1, 0.1)

# Train the network using a set of example inputs and targets
training_inputs = [[170, 70, 25], [160, 55, 30], [180, 90, 40], [150, 45, 20]]
training_targets = [[1], [0], [1], [0]]

for i in range(1000):
    for inputs, targets in zip(training_inputs, training_targets):
        network.train(inputs, targets)

# Test the network by making predictions on new inputs
test_inputs = [[175, 75, 27], [165, 60, 35], [185, 95, 42]]
for inputs in test_inputs:
    prediction = network.predict(inputs)
    print("Prediction:", prediction)
In this example, we train the network using a set of example inputs and targets. We iterate through the training data multiple times, updating the weights and biases after each iteration. After training, we test the network by making predictions on new inputs.

## Conclusion
Building a neural network from scratch has been a rewarding experience. It has deepened my understanding of the inner workings of neural networks, from the basics of neuron activation to the backpropagation algorithm for training. By implementing a neural network from scratch, I gained insights into the key concepts and challenges involved in designing and training a neural network.
While this neural network implementation is basic and not optimized for performance, I had fun while building this project and that is what matter ( plus all the benefits from learning).
now here is your cookie for reading this or scrolling down.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>




