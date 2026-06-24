# Multi-Layered Perceptron from Scratch
In the last project I built a perceptron from first principles, and there we encountered the mathematical limitation about a single-layered perceptron- geometrically it creates a linear decision boundary. This means a single perceptron can only separate data that is linearly separable. Hence, a perceptron can be seen as binary classifier that decides between two classes. <br>

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/62a4b7c7-b1c6-420f-9d9d-eac8b54a8139" />
<br>

A single perceptron resembles a neuron. To solve complex real world problems, we need a neural network which can solve non-linearly separable problems as well.
Non-linearly separable problems are solved using multiple boundaries.
<br>

A single neuron (a perceptron) can only create a single straight line as a decision boundary, which is why a single neuron fails completely at the XOR problem. The below image shows how a Multi-Layer Perceptron (a neural network with a hidden layer) solves XOR.

<img width="658" height="493" alt="image" src="https://github.com/user-attachments/assets/04b8de5e-128f-4a5d-b45e-e3ca97a94f2d" />
<br>
<br>

Let's understand how an MLP would solve the XOR problem and draw the above classification.<br>
We have four input pairs for the XOR gate: (0,0), (0,1), (1,0), (1,1).<br>
The hidden layer would have two neurons- to create the two decision boundaries and then the output layer would have one neuron which would give the final result.<br>
The two neurons in the hidden layer- compute parallely. Both the hidden neurons receive the exact same inputs.
- Hidden Neuron 1 multiplies them by its own set of weights and produces an output (Line 1).
- Hidden Neuron 2 multiplies them by its own distinct weights and produces a second output (Line 2).
<br>

These two outputs become the inputs for the final neuron (the output layer). This is very important to understand that- within the layer the neurons recieve the same inputs and compute parallelly, but the computation from one layer to the other is sequential because the output of the one becomes the input for the next.<br>

Lets further explore how the hidden layer neurons actually divide the space (something similar to this would be happening).

- Neuron 1: It draws the bottom line. It classifies everything above and to the right of this line (Green) as 1 and everything below this line (Purple) as 0. Thus, it successfully isolates the bottom-left point (0,0) into the Purple zone. But it incorrectly lumps the top-right point (1,1) into the Green zone.
- Neuron 2: It draws the top line. It classifies everything below and to the left of this line (Green) as 1 and everything above this line (Purple) as 0. Thus, it successfully isolates the top-right-point (1,1) into the Purple zone. But it incorrectly lumps the bottom-left point (0,0) into the Green zone.
<br>

<table>
  <tr>
    <td><img alt="neuron1" src="https://github.com/user-attachments/assets/a72d134d-e6df-4991-82bb-fc7f44d22279" width="400"/></td>
    <td><img alt="nueron2" src="https://github.com/user-attachments/assets/47376bc1-52e6-4af4-8180-cc556a149ed6"  width="400"/></td>
  </tr>
</table>
<br>

How the ouput neuron cleans it up- as of now both the neurons are making mistakes, individually. But when their outputs are sent into the output neuron, it performs AND operation. If a point lies in True zone for both the neurons then it is taken as True- in the Green zone, otherwise False- in the Purple zone.
<br>

The output neuron does not "know" that it has to perform AND operation. It arrives to that conclusion through backpropagation and gradient descent. We will explore these concepts later in this document.
<br>

Basically, the output neuron has a linearly separable problem for itself to solve. The problem for the output neuron has completely changed. 
