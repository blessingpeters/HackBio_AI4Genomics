# Activation Functions
Why Do We Need Activation Functions?
Imagine you are studying bacteria.

Suppose you discover that bacterial growth depends on:

Nutrient concentration
Temperature
Oxygen availability
A simple model might calculate:

Growth Score =
(Nutrients × Importance)
+
(Temperature × Importance)
+
(Oxygen × Importance)
This produces a number.

For example:

Growth Score = 85
But what does 85 mean?

Does the bacterium grow?

Does it not grow?

Does it grow rapidly?

We need a way to convert this raw score into a meaningful biological response.

This is exactly what an activation function does.

The Neural Network Problem
Recall what a neuron does.

A neuron receives inputs:

Input Features
       ↓
Weights
       ↓
Weighted Sum
Example:

Feature	Value	Weight
Age	40	0.2
BMI	30	0.5
Calculation:

(40 × 0.2)
+
(30 × 0.5)

=
8 + 15

=
23
The neuron produces:

23
This number is called the weighted sum.

But there is a problem.

The neuron has only performed multiplication and addition.

Mathematically, this is called a linear operation.

Why Is That a Problem?
Many biological systems are not linear.

For example:

Suppose nutrient concentration increases.

Does bacterial growth always increase proportionally?

No.

At some point:

Nutrients become saturated
Growth plateaus
Cells reach carrying capacity
Biology is full of non-linear relationships.

Examples:

Enzyme kinetics
Population growth
Drug responses
Gene regulation
Protein binding
Neural networks need a way to model these non-linear relationships.

Activation functions provide that ability.

A Simple Analogy
Imagine a laboratory door.

Students arrive at the entrance.

The door decides:

Can enter
or
Cannot enter
The door acts like a filter.

Input:

Student arrives
Decision:

Allowed?
Output:

Enter
or
Blocked
An activation function acts similarly.

It receives a number.

Then decides how much information should continue through the network.

What Does an Activation Function Do?
A neuron calculates:

Weighted Sum = 23
The activation function receives:

23
and transforms it into another value.

23
 ↓
Activation Function
 ↓
New Output
This new output is passed to the next layer.

The Most Popular Activation Function: ReLU
Almost every beginner CNN uses ReLU.

ReLU stands for:

Rectified Linear Unit
The rule is incredibly simple.

If value is negative → return 0

If value is positive → keep it
Examples:

Input: -5
Output: 0
Input: -2
Output: 0
Input: 4
Output: 4
Input: 10
Output: 10
ReLU as a Biological Switch
Think of ReLU like a gene.

Many genes behave like this:

Signal below threshold
↓
Gene OFF

Signal above threshold
↓
Gene ON
Similarly:

Input below zero
↓
OFF

Input above zero
↓
ON
ReLU acts like a simple biological switch.

Why Is ReLU Useful?
Suppose a neuron produces:

-50
This might represent:

No useful signal
ReLU converts it into:

0
Removing unnecessary information.

Meanwhile:

25
remains:

25
Preserving useful information.

Visualizing ReLU
Input:

-4  -2   0   2   4
Output:

 0   0   0   2   4
Everything below zero disappears.

Everything above zero survives.

ReLU in PyTorch
import torch
import torch.nn as nn

relu = nn.ReLU()

x = torch.tensor([-4, -2, 0, 2, 4])

print(relu(x))
Output:

tensor([0, 0, 0, 2, 4])
Another Activation Function: Sigmoid
Sigmoid behaves differently.

Instead of producing any number:

-100
to
100
it squeezes values between:

0 and 1
Examples:

Input: -10
Output: ~0
Input: 0
Output: 0.5
Input: 10
Output: ~1
Biological Analogy for Sigmoid
Imagine predicting whether a patient has a disease.

The model might produce:

Disease Probability = 0.92
or

Disease Probability = 0.08
Probabilities naturally fall between:

0 and 1
Sigmoid is useful when we want outputs that resemble probabilities.

ReLU vs Sigmoid
ReLU
Negative → 0

Positive → Keep value
Best for:

Hidden layers
Sigmoid
Always between 0 and 1
Best for:

Probability outputs
Why CNNs Use ReLU
Imagine a CNN analyzing handwritten digits.

The first layer may detect:

Edges
Corners
Lines
Curves
Some detected patterns are useful.

Some are not.

ReLU helps the network ignore weak or negative signals and focus on important patterns.

Without ReLU:

Layer 1
↓
Layer 2
↓
Layer 3
is mathematically equivalent to one giant linear equation.

The network becomes surprisingly limited.

With ReLU:

Layer 1
↓
ReLU
↓
Layer 2
↓
ReLU
↓
Layer 3
the network can learn complex biological and visual patterns.

A Simple Mental Model
Think of an activation function as a biological decision point.

Signal arrives
      ↓
Decision made
      ↓
Signal continues
Just as cells decide whether to:

Express a gene
Divide
Differentiate
Activate a pathway
an activation function decides:

Should this signal continue through the neural network?
That decision is what allows neural networks to learn complex patterns instead of behaving like simple calculators.