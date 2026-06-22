# Loss Functions and Optimizers

Why Do We Need Them?
Imagine you build a model to identify handwritten digits.

The model looks at an image and predicts:

Predicted Digit = 3
But the true digit is:

Actual Digit = 8
The model made a mistake.

Two questions now arise:

How wrong was the prediction?
How can the model improve?
The loss function answers the first question.

The optimizer answers the second.

Loss Function
A loss function measures how wrong the model's predictions are.

Think of it as the model's error score.

Prediction
      ↓
Loss Function
      ↓
Error Score
A small loss means:

Good prediction
A large loss means:

Poor prediction
Biological Analogy
Imagine measuring bacterial growth in an experiment.

You expected:

OD600 = 0.80
but observed:

OD600 = 0.25
The difference between expectation and observation is the error.

Loss functions measure this error during neural network training.

Cross Entropy Loss
For image classification tasks such as MNIST, the most common loss function is:

nn.CrossEntropyLoss()
It compares:

Predicted Class
vs
Actual Class
and calculates how wrong the prediction was.

Optimizer
The optimizer is responsible for improving the model.

After calculating the loss:

Prediction
      ↓
Loss
      ↓
Optimizer
      ↓
Model Update
the optimizer adjusts the network's weights so future predictions become more accurate.

Biological Analogy
Imagine performing a PCR experiment.

The result is poor.

You might adjust:

Annealing temperature
Mg²⁺ concentration
Primer concentration
Then repeat the experiment.

Each adjustment moves you closer to the desired result.

An optimizer does exactly the same thing.

It continuously adjusts the model's weights to reduce error.

Adam Optimizer
The most commonly used optimizer is:

torch.optim.Adam()
Adam automatically determines how much each weight should change during training.

For beginners, it is usually the best default choice.

The Training Cycle
Every neural network learns using the same loop:

Input Data
      ↓
Prediction
      ↓
Loss Function
      ↓
Calculate Error
      ↓
Optimizer
      ↓
Update Weights
      ↓
Better Prediction
This cycle repeats thousands of times until the model learns useful patterns.

Key Takeaways
Loss Function
Measures how wrong the model is.

Large Loss = Poor Prediction
Small Loss = Good Prediction
Optimizer
Improves the model by updating weights.

Loss
 ↓
Optimizer
 ↓
Better Weights
Simple Mental Model
Loss Function
=
Exam Marker

Optimizer
=
Student Learning From Feedback
The loss function tells the model how badly it performed.

The optimizer helps the model improve for the next attempt.