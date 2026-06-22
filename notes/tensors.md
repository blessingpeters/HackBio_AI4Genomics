# Why Are We Learning Tensors?
Imagine you perform an RNA-seq experiment.

You obtain expression values for 20,000 genes.

Gene	Expression
Gene1	12
Gene2	8
Gene3	20
...	...
Computers must store these values somehow.

For small numbers, a simple variable is enough:

expression = 12
But biological data usually contains thousands or millions of measurements.

To handle this efficiently, we use data structures such as vectors, matrices, and tensors.

From Scalars to Tensors
Everything begins with a scalar.

Scalar
A scalar is a single value.

Examples:

5
37
0.85
Biological examples:

Temperature = 37°C
OD600 = 0.85
pH = 7.2
Vector
A vector is a collection of numbers.

[5, 10, 15]
Example:

Gene expression from one sample:

[12, 8, 20, 15]
Think:

One sample
Many measurements
Matrix
A matrix is a table of numbers.

Example:

12  8
20 15
18 10
This could represent:

Gene	Sample1	Sample2
Gene1	12	8
Gene2	20	15
Gene3	18	10
Think:

Many samples
Many measurements
Tensor
A tensor is a generalization of vectors and matrices.

A simple way to think about it:

Scalar
↓
Vector
↓
Matrix
↓
Tensor
A tensor can have many dimensions.

For example:

Multiple matrices stacked together
Why Do We Need Tensors?
Modern biological and image datasets contain multiple dimensions.

Consider a microscopy image.

The image has:

Height
Width
A color image also has:

Red channel
Green channel
Blue channel
Now the data has three dimensions.

A tensor stores this naturally.

Tensors in PyTorch
PyTorch uses tensors for everything.

Create a tensor:

import torch

x = torch.tensor([1,2,3])
Output:

tensor([1,2,3])
Tensor Shapes
Every tensor has a shape.

Shape tells us how the data is organized.

Example:

x.shape
Output:

torch.Size([3])
Meaning:

3 values
Another example:

x = torch.tensor([
    [1,2],
    [3,4]
])

x.shape
Output:

torch.Size([2,2])
Meaning:

2 rows
2 columns
Tensor Shapes in Deep Learning
Suppose we have 10 patients.

Each patient has:

Age
BMI
Cholesterol
The tensor shape becomes:

[10,3]
Meaning:

10 patients
3 features
Tensor Shapes in Images
MNIST images are:

[28,28]
Meaning:

28 pixels high
28 pixels wide
If we have 64 images:

[64,28,28]
Meaning:

64 images
28 pixels high
28 pixels wide
PyTorch often adds a channel dimension:

[64,1,28,28]
Meaning:

64 images
1 channel
28 height
28 width
Always learn to interpret tensor shapes.

This is one of the most important deep learning skills.

What Is a Neural Network?
A neural network is a mathematical system that learns patterns from data.

Example:

Suppose we want to predict whether a patient has a disease.

Inputs:

Age
BMI
Blood Pressure
Output:

Disease
No Disease
The neural network learns how these inputs relate to the outcome.

The Artificial Neuron
The basic building block of a neural network is a neuron.

Think of it as a tiny calculator.

It receives inputs:

Age
BMI
Blood Pressure
Each input is assigned an importance.

These importance values are called weights.

Example:

Feature	Value	Weight
Age	40	0.2
BMI	28	0.8
BP	120	0.5
The neuron calculates:

(40 × 0.2)
+
(28 × 0.8)
+
(120 × 0.5)
Result:

8 + 22.4 + 60
=
90.4
This operation is called a weighted sum.

Neural Networks Are Layers of Neurons
Instead of using one neuron:

Input
 ↓
Neuron
 ↓
Output
we combine many neurons.

Input Layer
      ↓
Hidden Layer
      ↓
Output Layer
This creates a neural network.

What Flows Through a Neural Network?
Tensors.

Everything inside a neural network is a tensor.

Input:

[64,3]
64 patients.

3 features each.

Output:

[64,2]
64 predictions.

2 classes.

Neural networks do not see:

Patients
Genes
Images
They only see tensors.

Neural Networks as Tensor Transformers
A useful mental model:

Input Tensor
      ↓
Layer 1
      ↓
Tensor
      ↓
Layer 2
      ↓
Tensor
      ↓
Output Tensor
A neural network continuously transforms tensors into new tensors.

Example: MNIST Digit Recognition
Input image:

[1,28,28]
One grayscale image.

Batch of images:

[64,1,28,28]
64 images.

Neural network:

Image Tensor
      ↓
Layer 1
      ↓
Layer 2
      ↓
Layer 3
      ↓
Predictions
Output:

[64,10]
Meaning:

64 images
10 possible digits
The model predicts probabilities for:

0
1
2
3
4
5
6
7
8
9
PyTorch Example
Creating a tensor:

import torch

x = torch.rand(5,3)

print(x.shape)
Output:

torch.Size([5,3])
Meaning:

5 samples
3 features
Key Takeaways
A tensor is simply a container for numbers.

Scalar
↓
Vector
↓
Matrix
↓
Tensor
Neural networks consume tensors and produce tensors. Every input, output, weight, prediction, and image in PyTorch (our deep learning library) is represented as a tensor.

A neural network can be thought of as a machine that repeatedly transforms one tensor into another until a useful prediction is produced.

Understanding tensor shapes is one of the most important skills in deep learning because every layer in a neural network changes the shape of the data in some way.