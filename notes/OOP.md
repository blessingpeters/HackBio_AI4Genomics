### Object Oriented Programming (OOP)

# Object-oriented thinking as a life scientist
### Why Should a Life Scientist Care About OOP?
Imagine you are working with bacteria.

You know that:

Every bacterium has properties
Species
Growth rate
Antibiotic resistance
Every bacterium can perform actions
Grow
Divide
Respond to antibiotics
In biology, we naturally think of organisms as objects with properties and behaviors.

OOP does exactly the same thing in programming.

Instead of:

``` Bacteria
├── Properties
│   ├── Species
│   ├── Growth Rate
│   └── Resistance
│
└── Behaviors
    ├── Grow
    ├── Divide
    └── Die
```
We create:

class Bacteria:
    ...
And now our computer understands bacteria in a way similar to how we understand them.

This is why OOP is often easier for life scientists than for computer scientists.

You already think this way.

The Problem OOP Solves
Imagine you have 100 bacterial isolates.

Without OOP:

species_1 = "E.coli"
growth_rate_1 = 0.8

species_2 = "S.aureus"
growth_rate_2 = 0.4

species_3 = "P.aeruginosa"
growth_rate_3 = 0.6
After 100 isolates:

species_99
growth_rate_99
species_100
growth_rate_100
Absolute chaos.

OOP allows us to say:

class Bacteria:
    pass
and create bacteria whenever we need them.

The Four Main OOP Concepts
Everything in beginner OOP revolves around:

Class
Object
Attributes
Methods
Master these and you're 80% done.

What is a Class?
A class is a blueprint.

Think of it as a protocol.

Before you culture bacteria, you already know:

A bacterium should have:
- species
- growth rate
- resistance
This idea is a class.

class Bacteria:
    pass
We haven't created any bacteria yet.

We've only described what a bacterium should look like.

What is an Object?
An object is a real instance of a class.

Example:

class Bacteria:
    pass
Now create one:

ecoli = Bacteria()
Now:

ecoli
is an object.

Think:

Class = Species Description

Object = Actual Organism
Example:

Class
↓
Human

Objects
↓
Alice
Bob
Charlie
First Real Example
Create a class:

class Bacteria:
    pass
Create objects:

ecoli = Bacteria()
staph = Bacteria()
Now we have:

Object 1 → ecoli
Object 2 → staph
Even though both came from the same class.

Just like two bacteria can belong to the same species.

Attributes
Attributes are properties.

Example:

A bacterium has:

Species
Growth Rate
Resistance
Let's add them.

The init Function
This is the most important OOP concept.

Whenever an object is created:

ecoli = Bacteria()
Python automatically runs:

__init__()
Think of it as:

Birth of Object
Example:

class Bacteria:

    def __init__(self, species):
        self.species = species
Create object:

ecoli = Bacteria("E.coli")
Now:

print(ecoli.species)
Output:

E.coli
What is self?
This confuses everyone.

Don't overthink it.

Suppose:

ecoli = Bacteria("E.coli")
Python internally thinks:

ecoli.species = "E.coli"
The word:

self
simply means:

THIS OBJECT
Nothing more.

Example:

class Bacteria:

    def __init__(self, species):
        self.species = species
means:

Store species inside THIS bacterium
Multiple Attributes
Let's add more information.

class Bacteria:

    def __init__(self, species, growth_rate):
        self.species = species
        self.growth_rate = growth_rate
Create object:

ecoli = Bacteria("E.coli", 0.8)
Check values:

print(ecoli.species)
print(ecoli.growth_rate)
Output:

E.coli
0.8
Methods
Attributes store information.

Methods perform actions.

Biological analogy:

Species = Property

Grow() = Action
Example:

class Bacteria:

    def __init__(self, species):
        self.species = species

    def grow(self):
        print(self.species, "is growing")
Create bacterium:

ecoli = Bacteria("E.coli")
Run action:

ecoli.grow()
Output:

E.coli is growing
Adding More Biological Behavior
class Bacteria:

    def __init__(self, species):
        self.species = species

    def divide(self):
        print(self.species, "is dividing")
Use:

ecoli = Bacteria("E.coli")

ecoli.divide()
Output:

E.coli is dividing
Example: Cell Culture
Let's simulate cell growth.

class CellCulture:

    def __init__(self, cell_count):
        self.cell_count = cell_count

    def grow(self):
        self.cell_count = self.cell_count * 2

        print("Cells:", self.cell_count)
Create culture:

culture = CellCulture(100)
Grow:

culture.grow()
Output:

Cells: 200
Grow again:

culture.grow()
Output:

Cells: 400
Multiple Objects
One class can create many objects.

ecoli = Bacteria("E.coli")
staph = Bacteria("S.aureus")
pseudo = Bacteria("P.aeruginosa")
Each object stores its own data.

print(ecoli.species)
print(staph.species)
Output:

E.coli
S.aureus
Why OOP Matters for Deep Learning
Now we arrive at PyTorch.

A neural network is just another object.

Instead of bacteria:

class Bacteria:
    ...
we create:

class NeuralNetwork:
    ...
The network has:

Properties:

Weights
Biases
Layers
Actions:

Predict
Train
Evaluate
Exactly the same idea.

Inheritance
Now imagine:

Animal
├── Dog
├── Cat
└── Human
All are animals.

Instead of rewriting everything:

class Animal:
    ...
then:

class Dog(Animal):
    ...
Dog inherits Animal functionality.

Example

class Animal:

    def breathe(self):
        print("Breathing")
class Dog(Animal):
    pass
Create dog:

dog = Dog()
Run:

dog.breathe()
Output:

Breathing
Even though Dog never defined it.

It inherited it.

Why Inheritance Matters in PyTorch
Every neural network inherits from:

nn.Module
Example:

class SimpleCNN(nn.Module):
    ...
This means:

SimpleCNN
inherits
nn.Module
PyTorch gives us:

model training
parameter tracking
model saving
evaluation mode
for free.

super()
When inheriting, we must initialize the parent.

Example:

class SimpleCNN(nn.Module):

    def __init__(self):

        super().__init__()
Think:

Dear Parent Class,

Please initialize yourself first.
Then:

super().__init__()
runs.

Putting It All Together
This is essentially how every PyTorch model starts.

import torch.nn as nn

class SimpleCNN(nn.Module):

    def __init__(self):

        super().__init__()

        self.fc = nn.Linear(10, 2)

    def forward(self, x):

        return self.fc(x)
At this stage you do not need to understand:

Linear layer
Forward pass
Neural networks
Just observe the OOP structure.

Class
│
├── Inheritance
│
├── Constructor (__init__)
│
├── Attributes (self.fc)
│
└── Methods (forward)
Everything else in PyTorch is built on these ideas.

Mental Model for Life Scientists
Think of OOP exactly like biological taxonomy.

Class
↓
Species Description

Object
↓
Actual Organism

Attributes
↓
Traits

Methods
↓
Biological Behaviors

Inheritance
↓
Evolutionary Relationship

Constructor (__init__)
↓
Birth of Organism

self
↓
This Specific Organism