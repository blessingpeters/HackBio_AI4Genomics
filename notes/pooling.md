# Pooling and Fully Connected Layers

⚠️ This section will be further exemplified in subsequent functions during the coding videos
Learning Objectives
By the end of this lesson, you should be able to:

Understand why pooling layers are used
Understand how max pooling works
Explain how pooling reduces image size
Understand what flattening is
Understand the purpose of fully connected layers
Explain how CNNs make final predictions
Where Are We in a NN?
So far, we have learned that:

Image
 ↓
Convolution
 ↓
Activation Function
The convolution layer detects useful patterns.

Examples:

Edges
Corners
Curves
Lines
After detecting these features, we face a problem.

The feature maps can become very large.

Why Is This a Problem?
Imagine an image:

28 × 28 pixels
After several convolution operations, we may still have hundreds or thousands of values.

The neural network now has to process all of them.

This creates three problems:

Problem 1: More Computation
More numbers means:

More calculations
Training becomes slower.

Problem 2: More Memory
More numbers means:

More RAM
More GPU memory
Problem 3: Overfitting
The model may start memorizing training examples rather than learning useful patterns.

The Solution: Pooling
Pooling reduces the size of feature maps while preserving the most important information.

Think of pooling as image compression.

Instead of keeping every detail:

Keep important information
Discard unnecessary information
Biological Analogy
Imagine you are looking at a microscope slide.

Do you memorize every pixel?

No.

You summarize what matters.

You might say:

Large nucleus
Irregular membrane
High cell density
You compress thousands of observations into a few important features.

Pooling performs a similar task.

Max Pooling
The most common pooling operation is:

Max Pooling
The rule is simple:

Look at a small region

Keep only the largest value
Example
Suppose we have:

1   5
3   2
Max pooling examines all four values.

Largest value:

5
Output:

5
The other values are discarded.

Larger Example
Input:

1   5   2   4

3   2   1   0

8   6   4   2

5   3   7   1
Suppose we use a:

2 × 2 pooling window
First region:

1   5

3   2
Maximum:

5
Second region:

2   4

1   0
Maximum:

4
Third region:

8   6

5   3
Maximum:

8
Fourth region:

4   2

7   1
Maximum:

7
Output:

5   4

8   7
Notice:

4 × 4
↓
2 × 2
The image became much smaller.

Why Max Pooling Works
Suppose a feature map detects edges.

Original:

0 0 1 0
0 4 6 1
0 3 5 0
0 0 1 0
The largest values often represent the strongest detected features.

Pooling preserves those strong signals.

Max Pooling in PyTorch
import torch.nn as nn

pool = nn.MaxPool2d(2)
The number:

2
means:

Use a 2 × 2 window
What Happens After Pooling?
Eventually the CNN has extracted features such as:

Edges
Curves
Corners
Shapes
The model now needs to answer:

Which digit is this?
Pooling alone cannot do that.

We need a classifier.

Enter the Fully Connected Layer
A fully connected layer is responsible for making decisions.

Think of it as the final judge.

Biological Analogy
Imagine a pathologist reviewing tissue slides.

Earlier steps identify features:

Abnormal nucleus
High cell density
Membrane changes
The pathologist then combines all observations and decides:

Cancer
or
Not Cancer
The fully connected layer plays the same role.

Why Is It Called Fully Connected?
Suppose we have:

Neuron A
Neuron B
Neuron C
and

Output Neuron
Every input neuron connects to every output neuron.

A ─┐
B ─┼── Output
C ─┘
Everything is connected.

Hence:

Fully Connected
The Flattening Problem
Before entering a fully connected layer, we have feature maps.

Example:

32 feature maps

7 × 7 pixels each
Shape:

[32, 7, 7]
The fully connected layer cannot process this format directly.

Flattening
Flattening converts a multi-dimensional tensor into a single vector.

Example:

[32, 7, 7]
becomes:

[1568]
because:

32 × 7 × 7
=
1568
All values are placed into one long list.

Visualizing Flattening
Before:

Feature Map 1

1 2
3 4

Feature Map 2

5 6
7 8
After flattening:

[1,2,3,4,5,6,7,8]
Flattening in PyTorch
x = torch.flatten(x, start_dim=1)
or

nn.Flatten()
Fully Connected Layer
A fully connected layer is usually written as:

nn.Linear()
Example:

nn.Linear(1568, 128)
Meaning:

1568 input features

128 output features
Final Classification Layer
For MNIST:

Possible outputs:

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
Ten classes.

Final layer:

nn.Linear(128, 10)
Output:

[10]
One score for each digit.

CNN Pipeline
Putting everything together:

Input Image
      ↓
Convolution
      ↓
ReLU
      ↓
Pooling
      ↓
Convolution
      ↓
ReLU
      ↓
Pooling
      ↓
Flatten
      ↓
Fully Connected Layer
      ↓
Output Layer
      ↓
Prediction
MNIST Example
Input:

[1, 28, 28]
After convolution:

[16, 28, 28]
16 feature maps.

After pooling:

[16, 14, 14]
Size reduced.

After another pooling layer:

[32, 7, 7]
After flattening:

[1568]
After fully connected layer:

[128]
Final output:

[10]
One score for each digit.

Key Takeaways
Pooling layers help CNNs reduce feature-map size while preserving important information.

Max pooling keeps the strongest signal from a region.

Flattening converts feature maps into a single vector.

Fully connected layers act as the final decision-making component of the network.

A useful mental model is:

Convolution
↓
Find useful patterns

Pooling
↓
Compress useful patterns

Fully Connected Layer
↓
Make final decision
This division of labor is what allows CNNs to recognize complex visual patterns efficiently.