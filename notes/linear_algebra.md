# The Only Linear Algebra You Need Before Deep Learning
Most life scientists hear "linear algebra" and immediately think:

"This is going to be painful."

The good news is that for neural networks, CNNs, and machine learning, you only need a small subset of linear algebra.

In fact, if you understand:

Scalars
Vectors
Matrices
Tensors
Dot Products
Matrix Multiplication
you already understand about 90% of the linear algebra used in introductory deep learning.

Why Do We Need Linear Algebra?
Imagine you're studying bacterial growth.

You collect:

Sample	OD600
A	0.2
B	0.5
C	0.8
You have multiple numbers.

The question becomes:

How do we organize and manipulate many numbers efficiently?

Linear algebra is simply the mathematics of organizing and manipulating collections of numbers.

Nothing more.

Concept 1: Scalars
A scalar is a single number.

Examples:

5
0.75
42
Biological examples:

Cell count = 1000
OD600 = 0.8
pH = 7.2
Temperature = 37
All are scalars.

Visualization:

5
One number.

That's it.

Concept 2: Vectors
A vector is a collection of numbers.

Example:

[1, 2, 3]
Visualization:

[1 2 3]
Think of a vector as a list of measurements.

Example:

Three genes.

Gene	Expression
Gene A	5
Gene B	12
Gene C	8
Can be represented as:

[5, 12, 8]
That is a vector.

Why Vectors Matter
Every sample in machine learning is usually represented as a vector.

Example:

Patient:

Feature	Value
Age	40
BMI	28
Cholesterol	180
becomes:

[40, 28, 180]
The computer sees vectors everywhere.

Vector Length
The number of elements inside a vector.

Example:

[5, 10, 15]
Length:

3
Vector Operations
Suppose:

a = [1,2,3]
b = [4,5,6]
Addition:

a + b
becomes:

[5,7,9]
Element-by-element addition.

Biological analogy:

Gene expression from Experiment A:

[10, 20, 30]
Gene expression from Experiment B:

[5, 10, 15]
Combined:

[15,30,45]
Concept 3: Matrices
A matrix is a table of numbers.

Example:

[
 [1,2,3],
 [4,5,6]
]
Visualization:

1 2 3
4 5 6
Life scientists already use matrices every day.

RNA-seq count matrix:

Gene	Sample1	Sample2
GeneA	10	20
GeneB	5	8
GeneC	30	50
Internally:

10 20
 5  8
30 50
That's a matrix.

Rows and Columns
Consider:

10 20
 5  8
30 50
Rows:

10 20
5 8
30 50
Columns:

10
5
30
and

20
8
50
In bioinformatics:

Rows often represent:

Genes
Columns often represent:

Samples
Why Matrices Matter
Neural networks store weights in matrices.

Every neural network is essentially:

Input Matrix
×
Weight Matrix
=
Output Matrix
The entire field of deep learning rests on this idea.

Concept 4: Dimensions
Dimensions tell us shape.

Example:

10 20
 5  8
30 50
has:

3 rows
2 columns
Shape:

(3,2)
Read as:

3 × 2
Very important.

Whenever something breaks in PyTorch:

About 80% of the time:

Shape mismatch
is the culprit.

Concept 5: Dot Product
This is where neural networks begin.

Suppose:

inputs = [2,3]
weights = [4,5]
The dot product multiplies matching positions.

Step 1:

2 × 4 = 8
Step 2:

3 × 5 = 15
Step 3:

8 + 15 = 23
Result:

23
Why Dot Product Matters
Every neuron in a neural network performs a dot product.

Every.

Single.

Neuron.

Biological interpretation:

Suppose:

Feature	Value
Gene A	2
Gene B	3
Weights:

Gene	Importance
Gene A	4
Gene B	5
Neuron computes:

(2 × 4) + (3 × 5)
Result:

23
This becomes the neuron's output.

Neural networks are thousands of dot products happening simultaneously.

Concept 6: Matrix Multiplication
Now imagine many neurons working together.

Instead of:

One vector
we have:

Many vectors
This requires matrix multiplication.

Example:

Input:

1 2
3 4
Weights:

5 6
7 8
Multiply them.

Don't worry about calculating manually.

Focus on the idea:

Input Matrix
×
Weight Matrix
=
Output Matrix
This is what neural networks do.

Matrix Multiplication: The Core Operation Behind Neural Networks
Consider two matrices:

Matrix A
2	1	3
4	0	2
Matrix B
5	2
1	4
3	7
To calculate an element in the output matrix, we multiply a row from Matrix A by a column from Matrix B and then add the results together.

Example: Calculating the First Element
Take:

Row 1 of A

[2, 1, 3]
and

Column 1 of B

[5, 1, 3]
Multiply matching positions:

2 × 5 = 10
1 × 1 = 1
3 × 3 = 9
Add them together:

10 + 1 + 9 = 20
Therefore:

(AB)₁₁ = 20
This becomes the first element of the output matrix.

Visual Representation
Row from A:      [2  1  3]
                    ↓  ↓  ↓
Column from B:   [5  1  3]

(2×5) + (1×1) + (3×3)
= 10 + 1 + 9
= 20
The same process is repeated for every row-column combination until the entire output matrix is filled.

Why This Matters
Every neuron in a neural network performs this same operation.

A neural network layer is essentially a large matrix multiplication:

Input Features × Weights = Output Features

The only difference is that instead of multiplying a few numbers, modern neural networks may multiply millions of numbers simultaneously.

The key idea:

Each output value comes from:

One row
×
One column
This repeated operation powers every dense neural network layer.

Neural Network Interpretation
Imagine:

Input vector:

[Age, BMI, Cholesterol]
becomes:

[40, 28, 180]
The network has learned weights:

[
 [0.5,0.3],
 [0.2,0.8],
 [0.9,0.4]
]
Matrix multiplication combines them:

Input Features
×
Learned Weights
=
Predictions
That is literally what a neural network layer does.

Concept 7: What is a Tensor?
Life scientists often panic here.

Don't.

A tensor is simply a generalization of vectors and matrices.

Think:

Scalar
↓
Vector
↓
Matrix
↓
Tensor
Scalar

5
Vector

[1,2,3]
Matrix

[
 [1,2],
 [3,4]
]
Tensor

Many matrices stacked together.

Example:

Matrix 1
1 2
3 4

Matrix 2
5 6
7 8
Now we have a tensor.

Why CNNs Use Tensors
An MNIST image:

[28,28]
is a matrix.

A color image:

[3,224,224]
is a tensor.

Because:

Red channel
Green channel
Blue channel
are stacked together.

A batch of images:

[64,3,224,224]
is a larger tensor.

Meaning:

64 images
3 channels
224 height
224 width
PyTorch Shapes
You will constantly see:

x.shape
Example:

torch.Size([64,1,28,28])
Interpretation:

64 images
1 channel
28 pixels tall
28 pixels wide
Never memorize.

Always ask:

What does each dimension represent?

The Most Important Deep Learning Equation
Everything we have learned leads here:

Output = Input × Weights + Bias
A neuron receives:

Input
multiplies by:

Weights
adds:

Bias
produces:

Output
This single equation is responsible for nearly every prediction a neural network makes.

What You Must Remember
If your students remember only these ideas, they are ready for neural networks:

Scalars
Single numbers.

5
Vectors
Lists of numbers.

[1,2,3]
Matrices
Tables of numbers.

1 2
3 4
Tensors
Collections of matrices.

Used for images and batches.

Dot Product
Multiply corresponding values and sum.

Foundation of every neuron.

Matrix Multiplication
Many dot products happening simultaneously.

Foundation of every neural network layer.

Shapes
Always know:

x.shape
Most PyTorch errors are shape errors.

Mental Model for Life Scientists
Think of linear algebra as increasingly complex biological data structures:

Scalar
↓
Single measurement
(OD600)

Vector
↓
One sample
(Gene expression profile)

Matrix
↓
Many samples
(Expression matrix)

Tensor
↓
Many matrices
(Image batches)

Dot Product
↓
Importance-weighted biological signal

Matrix Multiplication
↓
Thousands of neurons processing data simultaneously
Once students understand this hierarchy, the transition to Neural Networks becomes surprisingly smooth because a neural network is simply a machine that repeatedly performs matrix multiplication and dot products on tensors.