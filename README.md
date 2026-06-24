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

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/cf9bd4eb-3d5b-432a-a08a-bb4806a5664a" />
<br>

The hidden layer would have two neurons- to create the two decision boundaries and then the output layer would have one neuron which would give the final result.<br>
The two neurons in the hidden layer- compute parallely. Both the hidden neurons receive the exact same inputs.
- Hidden Neuron 1 multiplies them by its own set of weights and produces an output (Line 1).
- Hidden Neuron 2 multiplies them by its own distinct weights and produces a second output (Line 2).
<br>

These two outputs become the inputs for the final neuron (the output layer). This is very important to understand that- within the layer the neurons recieve the same inputs and compute parallelly, but the computation from one layer to the other is sequential because the output of the one becomes the input for the next.<br>

Lets further explore how the hidden layer neurons actually divide the space (something similar to this would be happening).

- Neuron 1: It draws the bottom line. It classifies everything above and to the right of this line (Green) as 1 and everything below this line (Purple) as 0. Thus, it successfully isolates the bottom-left point (0,0) into the Purple zone. But it incorrectly lumps the top-right point (1,1) into the Green zone.
- Neuron 2: It draws the top line. It classifies everything below and to the left of this line (Green) as 1 and everything above this line (Purple) as 0. Thus, it successfully isolates the top-right-point (1,1) into the Purple zone. But it incorrectly lumps the bottom-left point (0,0) into the Green zone.

<table>
  <table border="1">
    <thead>
      <tr>
        <th>Input 1</th>
        <th>Input 2</th>
        <th>Output of Neuron 1</th>
        <th>Output of Neuron 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
      </tr>
      <tr>
        <td>1</td>
        <td>0</td>
        <td>1</td>
        <td>1</td>
      </tr>
      <tr>
        <td>0</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
      </tr>
    </tbody>
</table>
<br>

<table>
  <tr>
    <td><img alt="neuron1" src="https://github.com/user-attachments/assets/a72d134d-e6df-4991-82bb-fc7f44d22279" width="400"/></td>
    <td><img alt="nueron2" src="https://github.com/user-attachments/assets/47376bc1-52e6-4af4-8180-cc556a149ed6"  width="400"/></td>
  </tr>
</table>
<br>

The outputs of the first layer become the inputs for the second layer (the output neuron).
Basically, the output neuron now has a linearly separable problem for itself to solve.
<br>

<table>
  <table border="1">
    <thead>
      <tr>
        <th>Input 1 (output of neuron 1)</th>
        <th>Input 2 (output of neuron 2)</th>
        <th>Target output: XOR</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>0</td>
        <td>0</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1</td>
        <td>1</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1</td>
        <td>1</td>
      </tr>
      <tr>
        <td>0</td>
        <td>1</td>
        <td>0</td>
      </tr>
    </tbody>
</table>

<img width="500" alt="image" src="https://github.com/user-attachments/assets/216cf258-2632-4f43-9d2a-d566033c9aeb" />
<br>

The output neuron sees outputs of hidden as inputs. The 0s and 1s are now on opposite sides of one diagonal line. A single neuron can solve linearly separable data points and hence the problem is solved.
The hidden layer didn't just pass data through — it remapped 2D space into a new 2D space where the classes pulled apart. The output neuron inherits an easy problem.
<br>

The above graph doesn't resemble XOR- that is because the axes are no longer the original x₁ and x₂. They're outputs of the two hidden neurons. It's a completely different space.
The diagonal line does separate them cleanly. It's not supposed to look like XOR — it's a transformed version of the problem that the output neuron can solve with one line.
Green stops at the axes because x₁ and x₂ can only be 0 or 1 — they're neuron outputs (after activation), so valid coordinates only exist at the four corners: (0,0), (0,1), (1,0), (1,1).

<br>

<b>So what was the very first plot? </b>
<br>

That is the original XOR space (x₁, x₂) — not the hidden layer space. <br>

That shows what the full MLP has learned, mapped back onto the original input space. The decision boundary is now a diagonal band (two lines from the two hidden neurons combined), which is non-linear — that's why it looks different from the simple triangle.
The two hidden neurons each drew one line. The output neuron combined them. The result in original space = the overlap/band shape you see here.
So:
- Previous plot (triangle) = output neuron's view — simple one line
- That plot (band) = what the whole network learned mapped back to (x₁, x₂) — two lines combined
<br>

<b>How an MLP solves a non-linearly separable problem: </b>
<br>

- Classification means assigning labels to groups of data. Linearly separable classification is the special case where one line can separate those groups.
- Non-linearly separable problems are still classification problems. They simply require multiple transformations and/or multiple boundaries before the classes can be separated.
- A single neuron sees raw inputs and draws one line. That's all it can do. An MLP chains neurons into layers. The first hidden layer receives the raw inputs — but its outputs don't go to the answer. They go to the next layer as inputs. Each layer sees a transformed version of what the previous layer produced. The final output layer sees the most transformed version of all, and only then produces the answer.
- This chaining is everything. Each layer doesn't just process data, it repackages it into a simpler problem. The next layer doesn't work on the original problem. It works on a simpler version of it, handed down by the previous layer.
- The whole network shares one goal — the target output. But no single layer achieves it alone. The hidden layers aren't trying to classify; they're trying to produce a representation that makes classification easier for the layer after them.
- This is why depth matters. More layers means more transformations means more complex problems the network can untangle, one step at a time.
<br>

# Deep Dive into Multi-Layer Perceptron
# What information does a number need to carry so that we can later compute gradients automatically?
Imagine you have an expression like:
`f = (a * b) + c`
If a, b, and c are ordinary Python numbers (floats), Python computes the answer and gives you a final number. But after that computation, all the history is gone. The number f doesn't know that it came from a multiplication and an addition, it doesn't know which numbers participated in those operations, and it has no way to answer questions like, "If I change a by a tiny amount, how much will f change?"
<br>

For automatic differentiation, we cannot use a normal floating point number- because we need every number to remember its: numerical value, its gradient, how it was produced, who produced it.
So instead of storing plain floats, we store `Value` objects.
<br>

This is why we define `class Value`:
<br>

```
def __init__(self, data, _children=(), _op=''):
    self.data = data #actual numerical value (scalar)
    self._prev=set(_children) #input nodes that produce this result (Backward perspective)
    self._op=_op #operation string ('+', '*', etc)- operation that produced this node
    self.grad = 0 #how sensitive the final output is to this node
    self._backward=lambda:None
```
- Whenever a new instance (object) of the class is created- the `__init__` method is automatically invoked.
- Parameter 1: `data`- this is the actual scalar
- Parameter 2: `_children()`- this answers the question who created this object, this is the backward perspective, from the forward perspective it can be viewed as the parent node.
- Parameter 3: `_op=''`-this answers the question: which operation produced this node
- `_backward`: When backpropagation reaches a node, how does it know what derivatives to compute? Each node carries its own little derivative rule. This rule is stored in `self._backward`
Initially it is initalized with `none` because leaf nodes are not produced by any operation. Later every node replaces the `none` with the respective derivative rule. This rule decides how is the gradient sent backward.
-`grad`: it gives the answer to the question- how sensitive is the final output to this node?
<br>

A `Value` is a scalar that remembers both its past (how it was computed) and its future responsibility (how to propagate gradients).
<br>

# Local Gradients
<b>1. Addition </b>
<br>

`c = a + b`
<br>

What do local gradients represent? Local Gradient represents the the sensitivity of an isolated operation's output to a tiny change in one of its immediate inputs.
<br>

For example- local gradient for `a` (input) will tell how sensitive is `c` (output) to `a`, which means if we nudge `a` by a tiny amount how would that affect `c`? This is calculated using partial derivative- which means we keep the other input variable constant- so that we can measure the isolated effect of `a` on `c`, otherwise it will be a combined effect and it would become complex to find how much did each input contribute to this change.
<br>
For addition, local derivatives are:
```
∂c/∂a = 1
∂c/∂b = 1
```
This means that an addition node acts as a "gradient distributor." A nudge to any child node passes through to the parent node with 100% of its original strength, without being scaled or altered.
<br>

<b>2. Multiplication </b>
<br>

`c= a x b`

