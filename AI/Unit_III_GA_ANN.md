# UNIT III: GENETIC ALGORITHMS AND ARTIFICIAL NEURAL NETWORKS

## Comprehensive Master's Level Study Material

---

## TABLE OF CONTENTS

1. [Genetic Algorithms](#1-genetic-algorithms)
   - 1.1 Encoding Strategies
   - 1.2 Genetic Operators
   - 1.3 Fitness Functions and GA Cycle
   - 1.4 Problem Solving using GA
2. [Artificial Neural Networks](#2-artificial-neural-networks)
   - 2.1 Learning Paradigms
   - 2.2 Single Perceptron
   - 2.3 Multi-Layer Perceptron
   - 2.4 Self-Organizing Maps
   - 2.5 Hopfield Networks

---

# 1. GENETIC ALGORITHMS

## 1.1 Encoding Strategies

### 1.1.1 Fundamentals of Chromosome Encoding

**Definition**: Encoding is the process of representing a solution to a problem as a chromosome (genetic string) that genetic algorithm can manipulate.

**Key Concepts**:

```
Chromosome: Genetic representation of solution
├── Made up of sequence of genes
├── Each gene: Represents particular characteristic
├── Allele: Specific value of a gene
└── Genotype: Actual genetic encoding
    └── Phenotype: Actual solution representation

Example:
Problem: Find optimal values for x and y to maximize f(x,y) = x² + y²
Solution: x=3.5, y=2.1

Chromosome Encoding (Various methods):
├── Binary: 0011 0101 | 0010 0001
├── Real-valued: 3.5 | 2.1
├── Permutation: [1,3,2,4,5] (for ordering)
└── Tree: Expression tree (for GP)
```

**Importance of Encoding**:

```
1. Problem Representation:
   ├── Determines how solution space mapped to GA space
   ├── Affects search efficiency
   ├── Influences convergence behavior
   └── May include constraints/validity

2. Genetic Operators:
   ├── Encoding determines applicable operators
   ├── Different encodings need different crossover
   ├── Different encodings need different mutation
   └── Efficiency depends on encoding choice

3. Fitness Evaluation:
   ├── Must be computable from encoded chromosome
   ├── Decoding process determines speed
   ├── Accuracy of decoding affects results
   └── May include validity checking
```

### 1.1.2 Binary Encoding

**Description**: Chromosomes represented as strings of 0s and 1s

```
Structure:
Chromosome = [b₁ b₂ b₃ ... bₙ]
where each bᵢ ∈ {0, 1}

Example 1: Knapsack Problem (0/1 selection)

Problem: Select items to maximize value while staying within weight limit
├── Item 1: Value=10, Weight=2
├── Item 2: Value=20, Weight=4
├── Item 3: Value=15, Weight=3
└── Item 4: Value=25, Weight=5

Chromosome: [1, 0, 1, 1]
Interpretation:
├── Bit 1 = 1: Include Item 1
├── Bit 2 = 0: Exclude Item 2
├── Bit 3 = 1: Include Item 3
└── Bit 4 = 1: Include Item 4

Total Value = 10 + 15 + 25 = 50
Total Weight = 2 + 3 + 5 = 10 (within limit)

Example 2: Integer Optimization

Problem: Maximize f(x) where 0 ≤ x ≤ 15

Binary representation of integer x:
├── x = 5: [0,1,0,1] (binary 0101)
├── x = 10: [1,0,1,0] (binary 1010)
└── x = 15: [1,1,1,1] (binary 1111)

Decoding process:
Decimal value = b₀×2⁰ + b₁×2¹ + b₂×2² + b₃×2³

Example: [1,0,1,0]
Decimal = 1×1 + 0×2 + 1×4 + 0×8 = 5

Example 3: Gray Coding (Prevents Hamming Cliff Problem)

Issue with standard binary:
├── Small change in decimal → Large change in binary
├── Example: 7 (0111) vs 8 (1000) → 4 bits different
└── Called "Hamming cliff" or "Hamming wall"

Gray Code (Reflected Binary):
└── Each adjacent code differs by exactly 1 bit

Gray Code Conversion:
├── G₀ = B₀ (first bit same)
├── Gᵢ = Bᵢ XOR Bᵢ₊₁ (XOR with next bit)

Example: Decimal 7 vs 8
├── Standard binary: 0111 vs 1000 (4 bits differ)
├── Gray code: 0100 vs 1100 (1 bit differs)
└── Smoother search landscape

Advantages:
├── Simple to understand
├── Supports many crossover operators
├── Standard and well-tested
├── Each bit has clear meaning
├── Easy to generate random chromosomes
└── Supports standard mutation (bit flip)

Disadvantages:
├── Limited precision (need many bits for decimal accuracy)
├── Hamming cliff problem (without Gray coding)
├── More bits needed than real-valued encoding
├── Fixed range must be predetermined
└── Less natural for continuous problems
```

### 1.1.3 Real-Valued (Floating-Point) Encoding

**Description**: Chromosomes use actual real numbers directly

```
Structure:
Chromosome = [x₁, x₂, x₃, ..., xₙ]
where each xᵢ ∈ ℝ (real numbers)

Bounds:
├── Each gene may have lower bound Lᵢ
├── Each gene may have upper bound Uᵢ
└── Gene value: Lᵢ ≤ xᵢ ≤ Uᵢ

Example 1: Function Optimization

Problem: Minimize f(x,y) = (x-3)² + (y+2)²
Optimal: x=3, y=-2, f(3,-2)=0

Search space: -10 ≤ x ≤ 10, -10 ≤ y ≤ 10

Chromosomes (solutions):
├── Chromosome 1: [2.5, -1.8] → f ≈ 0.89
├── Chromosome 2: [3.1, -2.2] → f ≈ 0.02
└── Chromosome 3: [3.0, -2.0] → f = 0 (optimal)

Example 2: Neural Network Weights

Problem: Find optimal weights for neural network

Network has 5 weights: w₁, w₂, w₃, w₄, w₅

Chromosome: [0.234, -0.567, 0.123, 0.456, -0.789]

Each weight typically in range:
└── -1.0 ≤ wᵢ ≤ 1.0 (or [-0.5, 0.5], depends on initialization)

Advantages:
├── Natural representation for continuous problems
├── Requires fewer bits than binary for same precision
├── Faster computation (no conversion needed)
├── Better precision possible
├── More efficient for real-valued domains
├── Directly represents phenotype
└── Gradient information can be used

Disadvantages:
├── Requires different genetic operators
├── Needs careful crossover/mutation design
├── Gene interactions may be lost
├── May require domain knowledge to set bounds
└── Different parameter ranges need normalization
```

**Real-Valued Genetic Operators**:

```
Special operators for real-valued encoding:

Arithmetic Crossover:
└── Child value = a×Parent1 + (1-a)×Parent2
    where a ∈ [0,1] (usually 0.5)

Example:
├── Parent1: [2.0, 3.0, 4.0]
├── Parent2: [6.0, 9.0, 12.0]
├── With a=0.5:
└── Child: [4.0, 6.0, 8.0]

Blend Crossover (BLX-α):
└── Child value uniformly sampled from extended range
    Range = [min(P1,P2) - α×|P1-P2|, max(P1,P2) + α×|P1-P2|]

Example:
├── P1=2.0, P2=8.0, α=0.1
├── |P1-P2| = 6.0
├── Range = [2.0 - 0.6, 8.0 + 0.6] = [1.4, 8.6]
└── Child: random value in [1.4, 8.6]

Gaussian Mutation:
└── New value = Old value + N(0, σ²)
    where N(0,σ²) = Gaussian noise with std.dev σ

Example:
├── Original gene: 5.0
├── Noise: +0.2 (from Gaussian)
└── New gene: 5.2
```

### 1.1.4 Permutation Encoding

**Description**: Chromosome is sequence of distinct integers (order matters)

```
Used For: Ordering and arrangement problems

Structure:
Chromosome = [p₁, p₂, p₃, ..., pₙ]
where {p₁, p₂, ..., pₙ} = {1, 2, ..., n} (permutation)

Each position appears exactly once

Example 1: Traveling Salesman Problem (TSP)

Cities: A, B, C, D, E (5 cities)

Tour representation (cities visited in order):
├── Solution 1: [A, C, B, D, E]
├── Solution 2: [B, A, D, E, C]
└── Solution 3: [C, D, A, E, B]

Distance calculation:
├── Tour 1 distance: d(A→C) + d(C→B) + d(B→D) + d(D→E) + d(E→A)
├── Tour 2 distance: d(B→A) + d(A→D) + d(D→E) + d(E→C) + d(C→B)
└── Fitness: 1/distance (shorter tour = higher fitness)

Encoded as:
├── [1, 3, 2, 4, 5] (city indices)
├── [0, 2, 1, 3, 4] (0-indexed)
└── [C, A, E, B, D] (symbolic)

Example 2: Job Scheduling

Jobs: J1, J2, J3, J4, J5

Schedule (order to process):
├── Schedule 1: [J2, J1, J4, J3, J5]
├── Schedule 2: [J5, J3, J1, J2, J4]
└── Optimize: Minimize total processing time

Encoded: [2, 1, 4, 3, 5] or [5, 3, 1, 2, 4]

Example 3: Gene Assembly in Sequences

DNA fragments to arrange: [Frag1, Frag2, Frag3, Frag4]

Valid arrangement: [Frag3, Frag1, Frag4, Frag2]

Fitness: Overlap quality + match to reference sequence

Advantages:
├── Natural for combinatorial problems
├── Directly represents solution
├── All chromosomes valid (no repairs needed)
├── Clear correspondence to problem
└── Specific operators designed for this encoding

Disadvantages:
├── Standard crossover/mutation invalid (creates duplicates)
├── Requires special operators (PMX, OX, etc.)
├── More complex genetic operators needed
├── Limited operator choices
└── Harder to parallelize some operations
```

**Permutation-Specific Operators**:

```
Special operators prevent creation of invalid permutations:

Order Crossover (OX):
1. Select two random crossover points
2. Copy segment between points from first parent
3. Fill remaining positions with genes from second parent (left to right)

Example:
Parent1: [1 2 | 3 4 5 | 6 7]  (keep middle: 3,4,5)
Parent2: [4 5 | 6 7 1 | 2 3]

Child Construction:
├── Copy middle from P1: [?, ?, 3, 4, 5, ?, ?]
├── Fill from P2 (skip 3,4,5): [4, 5, 3, 4, 5, 6, 7]
└── Need to remove duplicates: [4, 5, 3, 6, 7, 1, 2] (valid permutation)

Partially Mapped Crossover (PMX):
1. Select two random points
2. Copy middle segment from first parent
3. Map genes from second parent to first parent's mapping
4. Fill remaining positions

Mutation - Inversion:
1. Select two random positions i and j
2. Reverse segment between i and j

Example:
Original: [1 2 | 3 4 5 6 | 7 8]
After inversion: [1 2 | 6 5 4 3 | 7 8]
Result: [1, 2, 6, 5, 4, 3, 7, 8]

Mutation - Displacement:
1. Select segment and new position
2. Move segment to new position

Example:
Original: [1 2 3 4 | 5 6 | 7 8]  (move 5,6 to position 2)
Result: [1 | 5 6 | 2 3 4 7 8]
```

### 1.1.5 Value Encoding

**Description**: Gene values represent actual attributes/parameters

```
Structure:
Chromosome = [v₁, v₂, v₃, ..., vₙ]
where each vᵢ can be string, letter, or other type

Used For: Problems with non-numeric parameters

Example 1: Neural Network Structure Design

Parameter representation:
├── Neuron 1: ["tanh", 10, 0.01]  (activation, # neurons, learning rate)
├── Neuron 2: ["relu", 5, 0.001]
├── Neuron 3: ["sigmoid", 8, 0.002]
└── ...

Chromosome: ["tanh", 10, 0.01, "relu", 5, 0.001, "sigmoid", 8, 0.002, ...]

Example 2: Algorithm Configuration

Problem: Configure parameters of classification algorithm

Chromosome:
├── Kernel type: "rbf" or "linear"
├── C parameter: 0.1, 1.0, 10.0
├── Gamma: 0.001, 0.01, 0.1, 1.0
└── Result: ["rbf", 10.0, 0.01]

Example 3: Robot Control Parameters

├── Motor speed: 0-100%
├── Direction: "forward", "backward", "left", "right"
├── Sensor mode: "IR", "ultrasonic", "camera"
└── Decision logic: "if-then-else", "fuzzy", "neural"

Chromosome: [75%, "forward", "IR", "fuzzy"]

Advantages:
├── Represents complex attributes naturally
├── No need for binary/real conversion
├── Directly expresses problem solution
├── Handles mixed data types
├── Flexible representation
└── Intuitive problem encoding

Disadvantages:
├── Requires custom genetic operators
├── Harder to design appropriate crossover
├── Mutation operations problem-specific
├── May have many combinations (large search space)
├── Harder to analyze mathematically
└── May need validity checking
```

### 1.1.6 Tree Encoding

**Description**: Chromosome is tree structure (used in Genetic Programming)

```
Structure:
Node: Can be function, operator, or terminal value
Tree: Nodes connected hierarchically

Example 1: Mathematical Expression

Expression: 2×x + 3×y

Tree representation:
         +
       /   \
      *     *
     / \   / \
    2   x 3   y

Chromosome: Encoded tree structure
├── Internal nodes: Operations (+, -, *, /)
├── Leaf nodes: Variables (x, y) or Constants (2, 3)
└── Evaluation: Traverse tree and compute

Example 2: Logic Expression

Expression: (A AND B) OR (NOT C)

Tree representation:
         OR
       /    \
      AND    NOT
      / \     |
     A   B    C

Chromosome: Tree with logic operations

Example 3: Control Programs

Program: IF temp > 20 THEN cool ELSE heat

Tree representation:
        COND
       /    \
      >      /\
     / \    /  \
   T  20  cool heat

Advantages:
├── Represents complex structures naturally
├── Handles variable-size solutions
├── Good for symbolic regression
├── Can represent programs/expressions
├── Scalable to complex problems
└── Biologically inspired

Disadvantages:
├── Complex genetic operators
├── Can suffer from bloat (trees grow too large)
├── Harder to analyze/understand
├── More computational overhead
├── Risk of invalid expressions after crossover
├── May need repair mechanisms
```

### 1.1.7 Analysis and Selection of Encoding

```
Factors to Consider When Choosing Encoding:

1. Problem Characteristics:
   ├── Nature of solution (continuous, discrete, mixed)
   ├── Problem constraints
   ├── Solution space structure
   └── Required precision

2. Search Space:
   ├── Size of search space
   ├── Connectivity (how close solutions are)
   ├── Landscape (smooth vs. rugged)
   └── Local optima prevalence

3. Computational Efficiency:
   ├── Encoding/decoding speed
   ├── Fitness evaluation time
   ├── Memory requirements
   └── Chromosome size implications

4. Operator Design:
   ├── Applicability of standard operators
   ├── Ease of custom operator design
   ├── Operator effectiveness
   └── Exploration vs. exploitation balance

5. Genetic Algorithm Performance:
   ├── Convergence speed
   ├── Solution quality
   ├── Population diversity maintenance
   └── Premature convergence avoidance

Summary Table:

| Encoding | Best For | Precision | Speed | Operators | Complexity |
|----------|----------|-----------|-------|-----------|------------|
| Binary | Discrete, theoretical | Low | Slow | Well-known | Low |
| Real | Continuous optimization | High | Fast | Custom needed | Medium |
| Permutation | TSP, scheduling | N/A | Medium | Special | High |
| Value | Mixed/complex | Variable | Variable | Problem-specific | High |
| Tree | Symbolic regression, GP | N/A | Slow | Complex | Very High |

Recommendation Process:

1. Analyze problem structure
2. Determine solution characteristics
3. Consider computational constraints
4. Evaluate available operators
5. Prototype with chosen encoding
6. Benchmark against alternatives
7. Fine-tune encoding if needed
```

---

## 1.2 Genetic Operators

### 1.2.1 Selection Operators

**Purpose**: Select individuals for reproduction; fitter individuals more likely to be selected.

#### 1.2.1.1 Roulette Wheel Selection

```
Concept: Probability of selection proportional to fitness

Mechanism:
1. Assign selection probability to each individual
2. Probability ∝ Fitness
3. Selection analogous to spinning roulette wheel
4. Fitter individuals have larger wheel segments

Formula:
Probability(i) = Fitness(i) / Σ(all fitness values)

Example:

Population: 4 individuals
├── Ind 1: Fitness = 10
├── Ind 2: Fitness = 20
├── Ind 3: Fitness = 15
└── Ind 4: Fitness = 5
Total Fitness = 50

Selection Probabilities:
├── Ind 1: 10/50 = 0.20 (20%)
├── Ind 2: 20/50 = 0.40 (40%)
├── Ind 3: 15/50 = 0.30 (30%)
└── Ind 4: 5/50  = 0.10 (10%)

Selection Process (Cumulative):
├── Ind 1: 0.00 to 0.20
├── Ind 2: 0.20 to 0.60
├── Ind 3: 0.60 to 0.90
└── Ind 4: 0.90 to 1.00

Selecting individuals (4 selections):
1. Random(0,1) = 0.75 → Ind 3 selected
2. Random(0,1) = 0.35 → Ind 2 selected
3. Random(0,1) = 0.10 → Ind 1 selected
4. Random(0,1) = 0.95 → Ind 4 selected

Result: Parents selected for reproduction

Pseudocode:
```
function roulette_wheel_selection(population, fitness_values, n_selections):
    total_fitness = sum(fitness_values)
    probabilities = fitness_values / total_fitness
    cumulative = cumsum(probabilities)
    selected = []
    
    for i = 1 to n_selections:
        r = random(0, 1)
        for each individual:
            if r < cumulative[individual]:
                selected.append(individual)
                break
    
    return selected
```

Advantages:
├── Fair selection based on fitness
├── Better individuals get more chances
├── Simple to implement
└── Natural fitness pressure

Disadvantages:
├── Premature convergence (if one super-fit individual)
├── Fitness scaling issues (very large differences)
├── Stochastic noise (good individuals might not be selected)
└── Requires positive fitness values
```

#### 1.2.1.2 Tournament Selection

```
Concept: Select subset of individuals, best wins

Mechanism:
1. Randomly choose k individuals (tournament size)
2. Select individual with highest fitness
3. Return selected individual
4. Repeat n times for n selections

Tournament Size k:
├── k=2: Binary tournament (most common)
├── k=3: Ternary tournament
├── k=4+: Larger tournaments
└── Larger k → Stronger selection pressure

Example (k=2):

Population: [Ind1(f=10), Ind2(f=20), Ind3(f=15), Ind4(f=5)]

Tournament 1:
├── Random pair: Ind2(20), Ind4(5)
└── Winner: Ind2 (higher fitness)

Tournament 2:
├── Random pair: Ind1(10), Ind3(15)
└── Winner: Ind3

Tournament 3:
├── Random pair: Ind2(20), Ind2(20)
└── Winner: Ind2

Tournament 4:
├── Random pair: Ind3(15), Ind4(5)
└── Winner: Ind3

Selected: [Ind2, Ind3, Ind2, Ind3]

Pseudocode:
```
function tournament_selection(population, fitness_values, n_selections, k):
    selected = []
    
    for i = 1 to n_selections:
        tournament = random_sample(population, k)
        winner = argmax_fitness(tournament)
        selected.append(winner)
    
    return selected
```

Properties:
├── Selection pressure tunable via k
├── No need for fitness scaling
├── Works with negative fitness
├── Parallelizable
├── No premature convergence issues
└── More genetic diversity maintained

Advantages:
├── Robust (works with any fitness scale)
├── Tunable selection pressure (via k)
├── Simple implementation
├── Better diversity maintenance
└── No fitness scaling needed

Disadvantages:
├── Less direct relationship to fitness (stochastic)
├── May need more tournaments than population size
└── Not proportional to fitness (similar fitnesses may lose)
```

#### 1.2.1.3 Rank Selection

```
Concept: Select based on rank, not absolute fitness

Mechanism:
1. Sort individuals by fitness
2. Assign ranks (1 to n)
3. Selection probability based on rank
4. Better ranked → Higher probability

Ranking Formula:
├── Linear ranking: Probability(rank i) = c - d×i
└── Exponential: Probability(rank i) = e^(-i/k)

Linear Ranking Example:

Sorted individuals (best first):
├── Rank 1: Ind2 (f=20) → Prob = c - d
├── Rank 2: Ind3 (f=15) → Prob = c - 2d
├── Rank 3: Ind1 (f=10) → Prob = c - 3d
└── Rank 4: Ind4 (f=5)  → Prob = c - 4d

With c=0.4, d=0.1:
├── Rank 1: 0.30
├── Rank 2: 0.20
├── Rank 3: 0.10
└── Rank 4: 0.0 (or small value)

Advantages:
├── Prevents super-fit individuals dominating
├── Maintains diversity better
├── Mitigates fitness scale problems
├── Selection pressure easily tunable
└── Avoids stagnation

Disadvantages:
├── Loses fitness information detail
├── All high-fitness individuals treated similarly
├── Linear ranking may be arbitrary
└── May lose good solutions
```

### 1.2.2 Crossover (Recombination) Operators

**Purpose**: Combine genetic material from two parents to create offspring.

#### 1.2.2.1 Single-Point Crossover

```
For Binary Encoding:

Mechanism:
1. Select random crossover point p (1 to n-1)
2. Create offspring by:
   ├── First part: From first parent (position 0 to p)
   ├── Second part: From second parent (position p+1 to n)

Example:

Parent 1: [1 0 1 | 1 0 1 0]
Parent 2: [0 1 0 | 0 1 1 1]
Crossover point: 3 (after position 2)

Offspring 1: [1 0 1 | 0 1 1 1] (P1 first, P2 second)
Offspring 2: [0 1 0 | 1 0 1 0] (P2 first, P1 second)

Visualization:
Parent1: 1 0 | 1 1 0 1 0
                |← point
Parent2: 0 1 | 0 0 1 1 1

Child1:  1 0 | 0 0 1 1 1 (crossed over)
Child2:  0 1 | 1 1 0 1 0 (crossed over)

Pseudocode:
```
function single_point_crossover(parent1, parent2):
    n = length(parent1)
    crossover_point = random_int(1, n-1)
    
    offspring1 = concatenate(
        parent1[0:crossover_point],
        parent2[crossover_point:n]
    )
    
    offspring2 = concatenate(
        parent2[0:crossover_point],
        parent1[crossover_point:n]
    )
    
    return offspring1, offspring2
```

Characteristics:
├── Simple to implement
├── Fast execution
├── May have positional bias
├── Good for short building blocks
└── Two offspring per operation

Disadvantages:
├── Positional bias (depends on crossover point position)
├── May break good building blocks
├── Limited exploration of combination space
└── Hamming distance may not be controlled
```

#### 1.2.2.2 N-Point Crossover

```
Generalization of single-point (multiple crossover points)

Two-Point Crossover:

Parent1: 1 0 | 1 1 0 | 1 0
           |       |
           p1      p2
Parent2: 0 1 | 0 0 1 | 1 1

Offspring1: 1 0 | 0 0 1 | 1 0 (take middle from P2)
Offspring2: 0 1 | 1 1 0 | 1 1 (take middle from P1)

Three-Point Crossover (p1, p2, p3):

Parent1: 1 | 0 1 1 | 0 1 | 0
Parent2: 0 | 1 0 0 | 1 1 | 1

Offspring1: 1 | 1 0 0 | 0 1 | 0
Offspring2: 0 | 0 1 1 | 1 1 | 1

General Formula:
N-point crossover has N randomly selected points
├── Segments alternate between parents
├── Offspring1: Seg1(P1), Seg2(P2), Seg3(P1), ...
└── Offspring2: Seg1(P2), Seg2(P1), Seg3(P2), ...

Advantages:
├── More flexible than single-point
├── Can preserve larger building blocks
├── Better exploration capability
├── Adaptable to problem structure
└── Balances different gene combinations

Disadvantages:
├── More complex to implement
├── Slightly slower than single-point
├── Too many points can be disruptive
└── Needs parameter tuning (number of points)
```

#### 1.2.2.3 Uniform Crossover

```
Each gene independently chosen from either parent

Mechanism:
1. For each position i in chromosome:
   ├── With probability p_cross: Take from Parent 1
   └── With probability (1-p_cross): Take from Parent 2

Example (p_cross = 0.5):

Parent1: 1 0 1 1 0 1 0
Parent2: 0 1 0 0 1 1 1

Mask:    1 0 1 0 1 0 1  (random binary mask)

Offspring: Each position:
├── Position 0: Mask=1 → Take P1[0]=1 → 1
├── Position 1: Mask=0 → Take P2[1]=1 → 1
├── Position 2: Mask=1 → Take P1[2]=1 → 1
├── Position 3: Mask=0 → Take P2[3]=0 → 0
├── Position 4: Mask=1 → Take P1[4]=0 → 0
├── Position 5: Mask=0 → Take P2[5]=1 → 1
└── Position 6: Mask=1 → Take P1[6]=0 → 0

Offspring: [1 1 1 0 0 1 0]

Pseudocode:
```
function uniform_crossover(parent1, parent2, p_cross=0.5):
    offspring = []
    
    for each position i:
        if random() < p_cross:
            offspring[i] = parent1[i]
        else:
            offspring[i] = parent2[i]
    
    return offspring
```

Characteristics:
├── High disruption (breaks long building blocks)
├── Good for fine-grained search
├── No positional bias
├── Uniform distribution
├── Best with linked operators

Advantages:
├── No positional bias
├── Good exploration
├── Simple to implement
├── Parallelizable
└── Effective for many problems

Disadvantages:
├── Very disruptive (may break good solutions)
├── Might need more generations
├── Can reduce convergence rate
└── Not suitable for all problems
```

#### 1.2.2.4 Arithmetic Crossover (Real-Valued)

```
For Real-Valued Encoding:

Blend Crossover (BLX-α):

Mechanism:
1. For each gene position:
   ├── Get values from both parents: v1, v2
   ├── Calculate range: [min(v1,v2), max(v1,v2)]
   ├── Expand by α: d = |v1 - v2|
   ├── New range: [min(v1,v2) - α×d, max(v1,v2) + α×d]
   └── New offspring value: Random from expanded range

Example:

Parent1: [2.0, 3.0, 4.0]
Parent2: [6.0, 9.0, 12.0]
α = 0.5

Gene 1: v1=2.0, v2=6.0
├── Min=2.0, Max=6.0, d=4.0
├── Range: [2.0-0.5×4.0, 6.0+0.5×4.0] = [0.0, 8.0]
└── Offspring: Random from [0.0, 8.0], say 3.5

Gene 2: v1=3.0, v2=9.0
├── Min=3.0, Max=9.0, d=6.0
├── Range: [3.0-0.5×6.0, 9.0+0.5×6.0] = [0.0, 12.0]
└── Offspring: Random from [0.0, 12.0], say 5.2

Gene 3: v1=4.0, v2=12.0
├── Min=4.0, Max=12.0, d=8.0
├── Range: [4.0-0.5×8.0, 12.0+0.5×8.0] = [0.0, 16.0]
└── Offspring: Random from [0.0, 16.0], say 9.8

Offspring: [3.5, 5.2, 9.8]

Extended Line Crossover (ELX):

More general form:
├── Offspring1: v1 + α × (v2 - v1)
├── Offspring2: v2 + α × (v1 - v2)

With α ∈ [-0.25, 1.25] for smooth interpolation/extrapolation

Advantages:
├── Preserves parent values
├── Can explore beyond parent range (α>0)
├── Biased toward parent region (α<1)
├── Flexible parameter control
└── Good for continuous optimization

Characteristics:
├── Creates offspring near/between parents
├── Parameter α controls expansion
├── Natural for real-valued problems
└── Works well with real-valued mutation
```

### 1.2.3 Mutation Operators

**Purpose**: Introduce random changes to maintain population diversity, prevent premature convergence.

#### 1.2.3.1 Bit-Flip Mutation (Binary)

```
Mechanism:
1. Select random position in chromosome
2. Flip bit: 0 → 1 or 1 → 0
3. Can repeat for multiple positions (controlled by mutation rate)

Example:

Original: [1 0 1 0 1 1 0]
Mutation point: Position 2

Mutated:  [1 0 0 0 1 1 0]  (position 2: 1→0)

Multiple Mutations (mutation rate pm=0.3, n=7):
Expected mutations: 7 × 0.3 = 2.1 ≈ 2

Pseudocode:
```
function bit_flip_mutation(chromosome, mutation_rate):
    mutated = copy(chromosome)
    
    for each position i in chromosome:
        if random() < mutation_rate:
            mutated[i] = 1 - mutated[i]  // flip bit
    
    return mutated
```

Mutation Rate Considerations:
├── Too low (pm < 0.01): Insufficient diversity
├── Typical (pm = 0.01-0.1): Balanced exploration
├── Too high (pm > 0.2): Random search, loses good traits
└── Adaptive: pm changes over generations

Probability Calculation:
├── Probability of no mutation: (1-pm)^n
├── For pm=0.01, n=100: (0.99)^100 ≈ 0.366 (36.6% unchanged)
├── For pm=0.1, n=100: (0.9)^100 ≈ 3×10^-5 (almost guaranteed change)
└── Optimal pm depends on problem

Advantages:
├── Simple and fast
├── Effective for binary encoding
├── Guaranteed exploration
└── Easy to implement

Disadvantages:
├── Can be destructive (high mutation rate)
├── Random changes may be useless
├── May disrupt good solutions
└── Needs careful parameter tuning
```

#### 1.2.3.2 Gaussian Mutation (Real-Valued)

```
Add random Gaussian noise to genes

Mechanism:
1. For each gene with probability pm:
   ├── Add Gaussian noise: N(0, σ²)
   └── New value = Old value + N(0, σ²)
2. May apply bounds (keep within [L, U])

Example:

Original: [2.5, 3.8, 1.2]
pm = 0.3 (30% mutation rate)
σ = 0.5 (standard deviation)

With probability 0.3 for each gene:
├── Gene 1 (mutate?): No
├── Gene 2 (mutate?): Yes → Add N(0,0.5²) ≈ +0.3 → 3.8+0.3 = 4.1
├── Gene 3 (mutate?): Yes → Add N(0,0.5²) ≈ -0.1 → 1.2-0.1 = 1.1

Mutated: [2.5, 4.1, 1.1]

Adaptive Mutation (Self-Adaptive):

Mutation rate adapts based on success:
├── If population improving: Increase σ (larger mutations)
├── If population stagnating: Decrease σ (smaller mutations)
└── Evolution strategies use self-adaptive σ

Pseudocode:
```
function gaussian_mutation(chromosome, sigma, mutation_rate):
    mutated = copy(chromosome)
    
    for each position i in chromosome:
        if random() < mutation_rate:
            noise = gaussian(0, sigma)
            mutated[i] = mutated[i] + noise
            if bounds defined:
                mutated[i] = clip(mutated[i], lower, upper)
    
    return mutated
```

Mutation Strength:
├── σ small (0.01-0.1): Fine-tuning near current solution
├── σ medium (0.1-1.0): Balanced exploration/exploitation
├── σ large (1.0+): Coarse search, may miss good areas
└── Typically: σ decreases as population converges

Advantages:
├── Natural for continuous problems
├── Smooth neighborhood exploration
├── Can be self-adaptive
├── Effective fine-tuning near optimum
└── Reduces destructive effect vs. random reset

Disadvantages:
├── Requires parameter tuning (σ)
├── Gaussian assumption may not fit problem
├── Small σ → slow convergence
├── Large σ → random jumps
└── Need to set appropriate bounds
```

#### 1.2.3.3 Insertion/Deletion Mutation (Permutation)

```
For Permutation Encoding:

Inversion Mutation (Most Common):

Mechanism:
1. Select two random positions i and j (i < j)
2. Reverse segment between i and j

Example:

Original: [1 2 | 3 4 5 6 | 7 8]
Position i=2, j=5

Mutated:  [1 2 | 6 5 4 3 | 7 8]

Reversal operation preserves all elements (still valid permutation)

Pseudocode:
```
function inversion_mutation(chromosome):
    mutated = copy(chromosome)
    i = random_int(0, len(chromosome)-1)
    j = random_int(i+1, len(chromosome))
    
    // Reverse segment [i:j]
    mutated[i:j] = reverse(mutated[i:j])
    
    return mutated
```

Displacement Mutation:

Mechanism:
1. Select segment to move
2. Select new position
3. Move segment, shift others

Example:

Original: [1 2 3 4 | 5 6 | 7 8] (move positions 4-5 to position 2)
Result:   [1 2 5 6 3 4 7 8]

Swap Mutation:

Mechanism:
1. Select two random positions
2. Swap elements

Example:

Original: [1 2 3 4 5]
Positions: 1 and 4

Mutated:  [1 4 3 2 5] (swapped positions 1 and 4)

Advantages (Permutation Mutation):
├── Maintains permutation property
├── Preserves diversity
├── Can escape local optima
├── Problem-specific operators
└── Effective for combinatorial problems

Disadvantages:
├── May not preserve good ordering segments
├── Effects problem-dependent
└── May need multiple operators
```

---

## 1.3 Fitness Functions and GA Cycle

### 1.3.1 Fitness Functions

**Definition**: Function that assigns quality measure (fitness value) to each individual, guiding evolution toward better solutions.

#### 1.3.1.1 Fitness Function Design

```
Key Characteristics:

1. Differentiable:
   ├── Should distinguish between good and bad solutions
   ├── Fitter individuals must be identifiable
   ├── Smooth gradients preferred (not always required)
   └── Too many equally-fit individuals → no guidance

2. Computable:
   ├── Must be efficiently calculable
   ├── Should not be bottleneck for GA
   ├── May accept approximations if exact is too expensive
   └── Time complexity critical (computed every generation)

3. Scalable:
   ├── Works for different problem sizes
   ├── Values don't grow uncontrollably
   ├── Allows consistent comparison
   └── Independent of absolute scale

4. Meaningful:
   ├── Reflects actual solution quality
   ├── Aligns with optimization objective
   ├── No misleading local optima
   └── Properly weights multiple objectives

5. Reliable:
   ├── Deterministic or low-noise
   ├── Consistent evaluation
   ├── No random evaluation errors
   └── Evaluation reflects true fitness
```

#### 1.3.1.2 Fitness Function Examples

```
Example 1: Function Optimization

Problem: Maximize f(x) = -(x-5)² + 25 where 0 ≤ x ≤ 10

Objective: Find x that maximizes f(x)
Optimal: x = 5, f(5) = 25

Fitness Function:
Fitness(x) = f(x) = -(x-5)² + 25

Sample Evaluations:
├── x=0: f(0) = -25 + 25 = 0 (poor)
├── x=5: f(5) = 0 + 25 = 25 (best)
├── x=10: f(10) = -25 + 25 = 0 (poor)
└── x=7.5: f(7.5) = -6.25 + 25 = 18.75 (good)

Example 2: Knapsack Problem

Problem: Select items maximizing total value while staying within weight limit
├── Weight limit: 15 kg
├── Items: [(V=10,W=2), (V=20,W=4), (V=15,W=3), (V=25,W=5)]
├── Objective: Maximize total value

Naive fitness = Total Value (but may exceed weight limit)

Better Fitness with Penalty:
```
if total_weight ≤ limit:
    fitness = total_value
else:
    fitness = total_value - penalty × (total_weight - limit)
```

Example Chromosomes:
├── [1,0,1,0]: V=10+15=25, W=2+3=5 → Fitness=25 (valid)
├── [1,1,1,1]: V=10+20+15+25=70, W=2+4+3+5=14 → Fitness=70 (valid)
├── [0,1,1,1]: V=20+15+25=60, W=4+3+5=12 → Fitness=60 (valid)
└── [1,1,1,1]: V=70, W=14 → Fitness=70 (optimal found)

Example 3: Neural Network Training

Problem: Train neural network to classify images

Fitness = 1 / (1 + Classification_Error)

Where Classification Error = (# misclassified) / (total samples)

Sample Neural Networks:
├── Network 1: Error = 0.05 → Fitness = 1/(1+0.05) = 0.952
├── Network 2: Error = 0.10 → Fitness = 1/(1+0.10) = 0.909
├── Network 3: Error = 0.20 → Fitness = 1/(1+0.20) = 0.833
└── Network 4: Error = 0.02 → Fitness = 1/(1+0.02) = 0.980 (best)

Example 4: Traveling Salesman Problem

Problem: Find shortest tour visiting all cities exactly once

Objective: Minimize distance

Fitness Function (convert to maximization):
Fitness(tour) = 1 / distance(tour)

Or:
Fitness(tour) = MAX_DISTANCE - distance(tour)

Sample Tours (5 cities):
├── Tour 1: Distance=100 km → Fitness = 1/100 = 0.01
├── Tour 2: Distance=50 km → Fitness = 1/50 = 0.02
├── Tour 3: Distance=30 km → Fitness = 1/30 = 0.033 (best)
└── Tour 4: Distance=80 km → Fitness = 1/80 = 0.0125

Example 5: Multi-Objective Optimization

Problem: Design car to maximize performance and minimize cost

Objectives:
├── Maximize acceleration (0-100 km/h in seconds) → minimize time
├── Minimize manufacturing cost ($)

Weighted Sum Fitness:
Fitness = w1 × (1/acceleration_time) + w2 × (1/cost)

With weights: w1=0.7, w2=0.3 (weight performance more)

Sample Designs:
├── Design A: 8s, $40k → Fitness = 0.7×(1/8) + 0.3×(1/40k) = 0.0875+0.0000075
├── Design B: 6s, $60k → Fitness = 0.7×(1/6) + 0.3×(1/60k) = 0.1167+0.000005
└── Design B preferred (higher fitness)

Pareto Ranking (for true multi-objective):
├── Non-dominated solutions get highest fitness
├── Dominated solutions get lower fitness
├── Encourages exploring Pareto frontier
```

#### 1.3.1.3 Fitness Scaling and Adjustment

```
Problem: Raw fitness values may be problematic

Issue 1: Large Range (Super-fit Individual Dominates)

Scenario:
├── Best fitness: 1,000,000
├── Worst fitness: 100
├── Super-fit individual gets ~99.99% selection probability
├── Population converges prematurely

Solution - Scaling:

Linear Scaling:
Scaled_Fitness = a × Raw_Fitness + b

Choose a, b such that:
├── Best individual: Scaled = c × average (e.g., c=1.5)
├── Average individual: Scaled = average
└── Worst individual: Scaled ≥ 0

Power Law Scaling:
Scaled_Fitness = Raw_Fitness^k (k < 1)

This "compresses" large differences

Example:
├── Raw: [100, 1000, 10000]
├── Power k=0.5: [10, 31.6, 100] (less extreme)
├── Power k=0.2: [2.51, 3.98, 6.31] (very compressed)

Issue 2: Insufficient Differentiation

Scenario:
├── All fitness values very close
├── [101, 102, 103, 104]
├── Selection ineffective (nearly uniform probabilities)

Solution - Ranking Selection:
└── Use rank instead of actual fitness values

Issue 3: Negative Fitness Values

Scenario:
├── Problem is minimization: Lower = Better
├── Values: 5, 10, 15, 20 (lower is better)
├── But GA prefers higher values
├── Roulette wheel needs positive values

Solution - Transformation:

Option 1 - Invert:
Fitness = 1 / value

Option 2 - Negate and Offset:
Fitness = MAX_VALUE - value + offset

Example with offset:
├── Original: [5, 10, 15, 20]
├── MAX_VALUE=20, offset=1
├── Transformed: [16, 11, 6, 1] (now higher is better)
```

### 1.3.2 The Genetic Algorithm Cycle

#### 1.3.2.1 Complete GA Process

```
Pseudocode - Classic Genetic Algorithm:

```
function genetic_algorithm():
    // Initialization Phase
    population ← initialize_random_population(pop_size)
    generation ← 0
    best_solution ← null
    best_fitness ← -infinity
    
    while termination_condition_not_met():
        // Evaluation Phase
        for each individual in population:
            individual.fitness ← evaluate_fitness(individual)
        
        // Track Best Solution
        for each individual in population:
            if individual.fitness > best_fitness:
                best_fitness ← individual.fitness
                best_solution ← copy(individual)
        
        // Selection Phase
        selected ← select_individuals(population, selection_method)
        
        // Crossover Phase
        offspring ← []
        for i=1 to population_size/2:
            parent1 ← selected[2*i-1]
            parent2 ← selected[2*i]
            
            if random() < crossover_probability:
                (child1, child2) ← crossover(parent1, parent2)
            else:
                (child1, child2) ← (copy(parent1), copy(parent2))
            
            offspring ← offspring + [child1, child2]
        
        // Mutation Phase
        for each individual in offspring:
            if random() < mutation_probability:
                individual ← mutate(individual)
        
        // Replacement Phase
        population ← replacement_strategy(population, offspring)
        generation ← generation + 1
    
    return best_solution
```

Phase Description:

1. **Initialization**:
   ├── Create initial population (usually random)
   ├── Size: Typically 50-500 individuals (problem-dependent)
   ├── Representation: Problem-specific encoding
   └── Goal: Cover diverse parts of search space

2. **Fitness Evaluation**:
   ├── Calculate fitness for each individual
   ├── Most expensive phase (repeated every generation)
   ├── May include constraint checking
   └── Comparison basis for selection

3. **Selection**:
   ├── Choose individuals for reproduction
   ├── Based on fitness (fitter → more likely)
   ├── Method: Roulette wheel, tournament, ranking
   └── Output: Selected pool for crossover

4. **Crossover**:
   ├── Combine genetic material from two parents
   ├── Probability: pc ∈ [0.5, 1.0] (typically 0.8-0.95)
   ├── If pc=1: All offspring undergo crossover
   ├── If pc<1: Some offspring copy parents directly
   └── Operator: Depends on encoding

5. **Mutation**:
   ├── Introduce random variation
   ├── Probability: pm ∈ [0.001, 0.1] (typically 0.01)
   ├── Per-gene or per-individual mutation rate
   ├── Maintains population diversity
   └── Prevents premature convergence

6. **Replacement**:
   ├── Decide how to form next generation
   ├── Strategy 1 (Generational): offspring replace parents
   ├── Strategy 2 (Steady-State): best individuals kept
   ├── Strategy 3 (Elitist): keep best, replace worst
   └── Affects evolution pressure

7. **Termination**:
   ├── Stop condition evaluation
   ├── Criteria: Generation limit, fitness threshold, no improvement
   └── Return best solution found
```

#### 1.3.2.2 Algorithm Flow Diagram

```
START
   ↓
Initialize Population
(Random chromosomes)
   ↓
Generate = 0
   ↓
┌─ MAIN LOOP ─────────────────┐
│                             │
│ Evaluate Fitness            │
│ For Each Individual         │
│                             │
│ Track Best Solution Found   │
│                             │
│ Selection                   │
│ (Roulette/Tournament/Rank)  │
│                             │
│ Crossover                   │
│ (Combine parent genes)      │
│                             │
│ Mutation                    │
│ (Random changes)            │
│                             │
│ Replacement                 │
│ (Form new generation)       │
│                             │
│ Generation++                │
│                             │
└─────────────────────────────┘
   ↓
Termination
Condition
Met?
   ├─ NO ──→ Go back to MAIN LOOP
   └─ YES
      ↓
Return Best Solution
   ↓
END
```

#### 1.3.2.3 Generation Progress Example

```
Problem: Maximize f(x) = -(x-5)² + 25, x ∈ [0,10]

Generation 0 (Initial Population):
├── Ind 1: x=2.3, f=19.81
├── Ind 2: x=7.8, f=18.72
├── Ind 3: x=1.0, f=9.00
├── Ind 4: x=9.0, f=9.00
├── Best: f=19.81

Generation 1:
After selection, crossover, mutation:
├── Ind 1: x=3.5, f=23.88
├── Ind 2: x=5.2, f=24.96
├── Ind 3: x=6.8, f=19.76
├── Ind 4: x=4.9, f=24.99
├── Best: f=24.99 (improved)

Generation 2:
├── Ind 1: x=5.05, f=24.9975
├── Ind 2: x=4.95, f=24.9975
├── Ind 3: x=5.10, f=24.99
├── Ind 4: x=5.00, f=25.00
├── Best: f=25.00 (optimal!)

Convergence Pattern:
├── Rapid improvement initially (good solutions found)
├── Slows as optimal approached
├── Population concentrates around best solution
├── Diversity decreases over time
```

#### 1.3.2.4 Replacement Strategies

```
Strategy 1: Generational GA (Generational Replacement)

Structure:
├── Each generation: Parents → Offspring replace Parents
├── Population size constant
├── All individuals replaced each generation

Pseudocode:
├── Offspring ← crossover(selected_parents)
├── Offspring ← mutation(offspring)
├── Population ← Offspring

Characteristics:
├── Completely new generation each iteration
├── May lose good solutions (if not elitist)
├── Faster evolution but higher variance
├── Standard GA approach
└── Useful for diverse population

Strategy 2: Steady-State GA

Structure:
├── Each generation: Add few offspring
├── Remove worst individuals
├── Population size constant
├── Gradual generational change

Pseudocode:
├── Selected ← tournament_selection(population, 2)
├── Offspring ← crossover(selected)
├── Offspring ← mutation(offspring)
├── worst_individual ← find_worst(population)
├── Population.replace(worst_individual, offspring)

Characteristics:
├── Continuous evolution (not generational)
├── Gradual population change
├── Better selection pressure
├── Individual focused
└── Useful for real-time applications

Strategy 3: Elitist GA (Elitism)

Structure:
├── Keep best k individuals unchanged
├── Evolve remaining population
├── Guarantees best solution never lost

Pseudocode:
├── Elites ← best_k_individuals(population, k)
├── Others ← remaining population
├── New_Others ← evolve(Others) via crossover/mutation
├── Population ← Elites + New_Others

With k=1 (most common):
├── Always keep single best solution
├── Guarantees monotonic improvement
├── Reduces diversity but ensures safety

Characteristics:
├── Preserves best solutions (greedy)
├── Monotonic improvement guaranteed
├── Less risky (won't lose best)
├── May converge prematurely
├── Recommended for most problems
```

---

## 1.4 Problem Solving Using GA

### 1.4.1 GA Application Framework

```
Steps to Apply GA to Problem:

1. Problem Formulation:
   ├── Define objective function
   ├── Identify variables/parameters
   ├── Specify constraints
   └── Determine problem bounds

2. Encoding Selection:
   ├── Choose representation (binary, real, permutation, etc.)
   ├── Map solutions to chromosomes
   ├── Plan encoding/decoding
   └── Verify all solutions representable

3. Fitness Function:
   ├── Design appropriate fitness measure
   ├── Ensure computational efficiency
   ├── Handle constraints (penalties if needed)
   ├── Test fitness function
   └── Verify alignment with objective

4. Operator Selection:
   ├── Choose genetic operators
   ├── Set crossover operator and probability
   ├── Set mutation operator and probability
   ├── Consider problem-specific operators
   └── Balance exploration/exploitation

5. Parameter Setting:
   ├── Population size: 50-500
   ├── Crossover probability: 0.6-0.95
   ├── Mutation probability: 0.001-0.1
   ├── Generations/iterations: Based on convergence
   └── Replacement strategy: Generational or steady-state

6. Implementation:
   ├── Code GA algorithm
   ├── Implement encoding/decoding
   ├── Implement operators
   ├── Test on simple cases
   └── Debug and optimize

7. Testing and Validation:
   ├── Run multiple GA runs (stochasticity)
   ├── Compare solutions (best, average, worst)
   ├── Analyze convergence behavior
   ├── Compare with known solutions/heuristics
   └── Sensitivity analysis on parameters

8. Optimization and Fine-Tuning:
   ├── Parameter tuning if needed
   ├── Operator adaptation
   ├── Local search integration
   └── Performance optimization
```

### 1.4.2 Detailed Example: Traveling Salesman Problem

```
Problem Definition:

TSP: Find shortest tour visiting n cities exactly once, return to start

Cities: A, B, C, D, E
Distance Matrix (symmetric):
        A    B    C    D    E
    A [ 0   10   15   20   30]
    B [10    0   35   25   15]
    C [15   35    0   30   20]
    D [20   25   30    0   10]
    E [30   15   20   10    0]

Optimal Tour: A-B-E-D-C-A with distance: 10+15+10+30+15 = 80

Step 1: Problem Formulation

Objective: Minimize total tour distance
Variables: Tour order (5! = 120 possible tours)
Constraints: Visit each city exactly once
Domain: Permutations of cities

Step 2: Encoding Selection

Permutation Encoding (Natural):
├── Chromosome: Sequence of city indices [1,2,3,4,5]
├── Example: [2,4,1,5,3] means tour B-D-A-E-C
├── All valid permutations represent valid tours
└── No infeasible solutions

Step 3: Fitness Function

Objective: Minimize distance → Maximize fitness

Design Option 1:
Fitness(tour) = 1 / total_distance

Design Option 2:
Fitness(tour) = MAX_DISTANCE - total_distance

Or normalize:
Fitness(tour) = 1 - (distance - min_distance)/(max_distance - min_distance)

Example:
├── Tour [1,2,3,4,5]: Distance = 10+35+30+10+30 = 115
├── Fitness = 1/115 = 0.0087
├── Tour [2,5,4,3,1]: Distance = 15+10+30+15+10 = 80
├── Fitness = 1/80 = 0.0125 (better)

Calculate_distance Pseudocode:
```
function calculate_distance(tour, distance_matrix):
    total_distance = 0
    n = length(tour)
    
    for i = 0 to n-1:
        from_city = tour[i]
        to_city = tour[(i+1) mod n]
        total_distance += distance_matrix[from_city][to_city]
    
    return total_distance
```

Step 4: Operator Selection

Crossover: Order Crossover (OX)
├── Preserves city order sequences
├── Designed for permutation problems
└── Probability: pc = 0.9

Mutation: Inversion (2-opt style)
├── Reverse segment of tour
├── Escapes local optima
└── Probability: pm = 0.05

Step 5: Parameter Setting

Population size: n_pop = 50
Crossover probability: pc = 0.9
Mutation probability: pm = 0.05
Number of generations: max_gen = 100
Replacement: Elitist (keep best)

Step 6: GA Execution

Generation 0:
Generate 50 random tours
├── Tour 1: [1,2,3,4,5] → Distance = 115
├── Tour 2: [5,3,1,4,2] → Distance = 98
├── Tour 3: [3,5,2,1,4] → Distance = 105
├── ...
├── Tour 50: [4,2,5,1,3] → Distance = 92
└── Best so far: [4,2,5,1,3] → 92

Generation 1:
Select best individuals
├── Tournament selection: pick winners
Crossover:
├── [4,2,5,1,3] × [1,3,2,4,5] → [4,2,5,3,1] + [1,3,2,4,5] → Dist=85,140
Mutation:
├── Invert segment: [4,2,5,3,1] → [4,5,2,3,1] → Dist=88
Evaluate new population
├── Best: [4,2,5,3,1] → 85 (improved!)

... (generations 2-100) ...

Generation 50:
Population convergence
├── Most individuals: tours near optimal
├── Best: [2,5,4,3,1] or similar → Dist=80
└── Little diversity

Generation 100:
└── Best found: [2,5,4,3,1] → Dist=80 (optimal!)

Step 7: Results Analysis

Final Solution: [2,5,4,3,1] (cities B-E-D-C-A)
Distance: 80
Optimality: Best known = 80 (optimal!)
Convergence: 85 generations to optimal

Multiple Runs:
├── Run 1: 80 (50 generations)
├── Run 2: 80 (75 generations)
├── Run 3: 82 (100 generations, near-optimal)
├── Average: 80.67
└── Best: 80
```

### 1.4.3 Real-World Applications

```
Application 1: Function Optimization

Problem: Minimize complex multi-dimensional function
├── Rosenbrock: f(x,y) = (1-x)² + 100(y-x²)²
├── Variables: Multiple parameters
├── Domain: Real-valued

GA Approach:
├── Encoding: Real-valued chromosomes
├── Population: 100-200 individuals
├── Operators: Blend crossover, Gaussian mutation
├── Fitness: 1/(1+f(x)) for minimization problems
└── Result: Finds global/local optimum

Performance vs. Other Methods:
├── GA: Robust to multimodal, no derivative needed
├── Gradient Descent: Fast but may get stuck locally
├── Random Search: Works but slow
└── GA good when derivatives unavailable

Application 2: Machine Learning - Feature Selection

Problem: Select best features for classification
├── Dataset: 50 features total
├── Task: Find subset reducing dimensionality
├── Objective: Maximize classification accuracy

GA Approach:
├── Encoding: Binary (1=include, 0=exclude)
├── Chromosome length: 50 bits
├── Fitness: Classification accuracy on validation set
├── Population: 50 individuals
└── Result: Feature subset that balances accuracy/complexity

Example:
├── Initial: Random feature subsets
├── Generation 50: Accuracy 85%
├── Generation 100: Accuracy 91%
├── Final: Selected 20 features with 92% accuracy

Application 3: Neural Network Training

Problem: Train neural network for image classification
├── Network: 100 neurons, 2 hidden layers
├── Weights: 1000+ parameters to optimize
├── Dataset: MNIST (60k training images)
├── Objective: Minimize classification error

GA Approach:
├── Encoding: Real-valued (one gene per weight)
├── Chromosome length: 1000+ genes
├── Fitness: 1/(1+error_rate)
├── Population: 30-50 networks
├── Operators: Real-valued crossover, Gaussian mutation
└── Training: 100-200 generations

vs. Backpropagation:
├── GA: Slower, but handles multimodal, no local gradients needed
├── Backprop: Faster, standard method, gradient-based
├── Hybrid: Use GA for structure, backprop for weights

Application 4: Scheduling and Optimization

Problem: Schedule jobs on machines minimizing total time

Instance:
├── Jobs: 20 jobs with durations
├── Machines: 5 identical machines
├── Objective: Minimize maximum completion time (makespan)

GA Approach:
├── Encoding: Permutation (job order) + assignment
├── Chromosome: [Job sequence, Machine assignments]
├── Fitness: 1/makespan
├── Population: 100 individuals
├── Operators: Job order crossover, machine reassignment mutation
└── Result: Job schedule across 5 machines

Example Schedule:
├── Machine 1: Jobs [3,7,11] → Finish time: 45
├── Machine 2: Jobs [1,5,9,13] → Finish time: 50
├── Machine 3: Jobs [2,6,10] → Finish time: 48
├── Machine 4: Jobs [4,8,12] → Finish time: 52
├── Machine 5: Jobs [14,15,16,17] → Finish time: 55
├── Makespan: 55 (maximum)
```

---

# 2. ARTIFICIAL NEURAL NETWORKS

## 2.1 Learning Paradigms

### 2.1.1 Supervised Learning

**Definition**: Learning from labeled examples (input-output pairs).

```
Structure:
Training Data:
├── Examples: (x₁, y₁), (x₂, y₂), ..., (xₙ, yₙ)
├── xᵢ: Input vector (features)
├── yᵢ: Target output (label/value)
└── Both input and output known

Goal:
├── Learn function f: x → y
├── Minimize prediction error
├── Generalize to unseen data

Process:
    Input x
      ↓
   Neural
   Network
      ↓
   Output ŷ (predicted)
      ↓
   Compare with Target y
      ↓
   Calculate Error = y - ŷ
      ↓
   Backpropagation
      ↓
   Update Weights
```

**Supervised Learning Tasks**:

```
1. Classification: Predict category/class

Binary Classification:
├── Example: Email (spam/not spam)
├── Output: y ∈ {0, 1} or {-1, 1}
├── Loss: Cross-entropy, hinge loss
└── Network output: Single neuron with sigmoid

Multi-class Classification:
├── Example: Digit recognition (0-9)
├── Output: y ∈ {1,2,...,K} (K classes)
├── Loss: Cross-entropy
└── Network output: K neurons with softmax

Example Network:
    Input Layer (784 neurons for 28×28 images)
         ↓
    Hidden Layer 1 (128 neurons, ReLU)
         ↓
    Hidden Layer 2 (64 neurons, ReLU)
         ↓
    Output Layer (10 neurons, Softmax) for digits 0-9

2. Regression: Predict continuous value

Examples:
├── House price prediction from features
├── Stock price forecasting
├── Temperature prediction
├── Demand forecasting

Output:
├── y ∈ ℝ (real number)
├── Loss: Mean Squared Error (MSE)
└── Network output: Linear activation

Example Network:
    Input Layer (5 features: size, location, age, rooms, condition)
         ↓
    Hidden Layer (20 neurons, ReLU)
         ↓
    Hidden Layer (10 neurons, ReLU)
         ↓
    Output Layer (1 neuron, Linear) → Price
```

**Supervised Learning Workflow**:

```
Step 1: Data Collection
├── Gather examples
├── Label each example
└── Ensure quality labels

Step 2: Data Preprocessing
├── Normalize/standardize features
├── Handle missing values
├── Remove outliers
└── Feature scaling

Step 3: Train-Test Split
├── Training set: 70-80% (learn from this)
├── Validation set: 10% (tune hyperparameters)
├── Test set: 10-20% (evaluate performance)

Step 4: Model Training
├── Initialize weights randomly
├── Feed forward training samples
├── Calculate loss
├── Backpropagate error
├── Update weights
└── Repeat until convergence

Step 5: Validation
├── Evaluate on validation set
├── Check for overfitting
├── Adjust hyperparameters if needed
└── Continue training if necessary

Step 6: Testing
├── Evaluate on test set (unseen data)
├── Report final performance
├── Compare with baseline methods
└── Deploy if satisfactory

Performance Metrics:

Classification:
├── Accuracy: (TP + TN) / (TP + TN + FP + FN)
├── Precision: TP / (TP + FP)
├── Recall: TP / (TP + FN)
├── F1-score: 2 × (Precision × Recall) / (Precision + Recall)
└── Confusion Matrix: Shows true/false positives/negatives

Regression:
├── MAE (Mean Absolute Error): (1/n) × Σ|yᵢ - ŷᵢ|
├── MSE (Mean Squared Error): (1/n) × Σ(yᵢ - ŷᵢ)²
├── RMSE (Root MSE): √MSE
└── R²: Coefficient of determination
```

### 2.1.2 Unsupervised Learning

**Definition**: Learning from unlabeled data; find patterns/structure.

```
Structure:
Training Data:
├── Examples: x₁, x₂, ..., xₙ
├── Only inputs (no labels)
├── No target output
└── Unknown structure

Goal:
├── Discover inherent structure
├── Group similar examples
├── Reduce dimensionality
├── Find patterns/relationships

Process:
    Input Data (unlabeled)
      ↓
   Neural Network
      ↓
   Discover Patterns/Clusters
      ↓
   Output (cluster labels, representations, etc.)
```

**Unsupervised Learning Tasks**:

```
1. Clustering: Group similar examples

K-Means:
├── Partition data into k clusters
├── Minimize within-cluster distance
├── Maximize between-cluster distance
└── Determine optimal k

Example:
    Customer Segmentation (unlabeled customer data)
    ├── Feature 1: Annual spending
    ├── Feature 2: Visit frequency
    └── Discover: 3 customer types
        ├── High value (high spend, frequent)
        ├── Occasional (medium spend, rare)
        └── Low value (low spend, rare)

Hierarchical Clustering:
├── Create tree of clusters
├── Visualize dendrogram
├── Choose cut level for cluster count
└── Agglomerative or divisive

2. Dimensionality Reduction: Compress data

Principal Component Analysis (PCA):
├── Find directions of maximum variance
├── Keep top k components
├── Reduce from d to k dimensions (k << d)
└── Preserve most information

Example:
    Image compression
    ├── 28×28 pixel image = 784 features
    ├── PCA finds important features
    ├── Reduces to 50 principal components
    └── Retains ~95% variance

Autoencoders:
├── Neural network learns compressed representation
├── Bottleneck layer (hidden layer) = compressed form
├── Encoder: x → h (compress)
├── Decoder: h → x' (reconstruct)
└── Minimize reconstruction error

3. Association Rule Mining: Find relationships

Market Basket Analysis:
├── Items purchased together
├── Discover patterns: "If buy X, likely buy Y"
├── Support: P(X ∧ Y)
├── Confidence: P(Y|X)
└── Applications: Cross-selling, product placement

4. Anomaly Detection: Find unusual examples

Example:
    Fraud detection (unlabeled data)
    ├── Learn normal transaction patterns
    ├── Flag transactions far from normal
    ├── Threshold-based detection
    └── Minimize false positives
```

**Self-Organizing Neural Networks** (Often Unsupervised):

```
Self-Organizing Maps (SOM / Kohonen Maps):
├── Competitive learning
├── Neurons organized in 2D grid
├── Similar inputs map to nearby neurons
├── Topological ordering preserved
└── Used for visualization and clustering

Hebbian Learning:
├── "Neurons that fire together, wire together"
├── Strengthen connections between co-activated neurons
├── Unsupervised rule: Δw ∝ yᵢ × yⱼ
└── Used in various unsupervised networks
```

### 2.1.3 Reinforcement Learning

**Definition**: Learning through interaction and rewards; agent learns optimal behavior.

```
Structure:
├── Agent: Learning entity
├── Environment: Responds to agent actions
├── State: Current situation
├── Action: Agent's choice
├── Reward: Feedback on action quality
└── Goal: Maximize cumulative reward

Process:
    Agent observes State S
         ↓
    Agent selects Action A
         ↓
    Environment transitions to State S'
         ↓
    Agent receives Reward R
         ↓
    Agent updates policy based on (S,A,R,S')
         ↓
    Repeat until goal achieved
```

**RL Paradigms**:

```
1. Model-Free Learning (No environment model)

Q-Learning:
├── Learn Q-values: Q(s,a) = expected return from (state,action)
├── TD update: Q(s,a) ← Q(s,a) + α(r + γ × max Q(s',a') - Q(s,a))
├── α: Learning rate
├── γ: Discount factor (future rewards weight)
└── Converges to optimal policy

Example - Game Playing:
    State: Current board position
    Action: Possible moves
    Reward: +1 win, -1 loss, 0 draw
    Learn: Q(board_position, move) values
    Policy: Choose action with max Q-value

SARSA (State-Action-Reward-State-Action):
├── On-policy learning (learns from actual actions taken)
├── Update: Q(s,a) ← Q(s,a) + α(r + γ × Q(s',a') - Q(s,a))
├── a' is actually-selected next action (not max)
├── More conservative than Q-learning
└── Better for online learning

2. Policy-Based Learning (Learn policy directly)

Policy Gradient:
├── Represent policy: π(a|s) = P(action|state)
├── Gradient: ∇J(θ) ∝ E[∇ log π(a|s) × R]
├── Update: θ ← θ + α × ∇J(θ)
├── θ: Policy parameters (weights)
└── Suitable for continuous actions

Actor-Critic:
├── Actor: Policy (what action to take)
├── Critic: Value function (how good is state)
├── Actor updates: Policy gradient
├── Critic updates: TD learning
└── Complementary components

3. Model-Based Learning (Learn environment model)

├── Learn model: P(s'|s,a), R(s,a)
├── Plan: Use model to find good policy
├── Method: Value iteration, Policy iteration
└── More sample-efficient but computationally harder
```

**RL Example: Robot Navigation**

```
Problem: Robot learns to navigate to goal

State Space:
├── Robot position (x, y)
├── Goal position (fixed)
├── Obstacles (static)
└── Continuous or discrete grid

Action Space:
├── Move forward, backward, left, right
├── Or continuous: Steering angle, speed

Reward Function:
├── -1 per step (penalize long paths)
├── +100 reaching goal
├── -50 hitting obstacle
└── Goal: Maximize total reward

Learning Process:
    Generation 1:
    ├── Random actions: Bumps into obstacles frequently
    ├── Few rewards: Reach goal occasionally by luck
    └── Low average reward

    Generation 100:
    ├── Learned obstacle locations
    ├── Planned basic paths
    ├── Average reward improved
    └── Still suboptimal

    Generation 1000:
    ├── Optimal policy learned
    ├── Navigates efficiently to goal
    ├── Avoids obstacles
    └── High average reward

Comparison with Supervised:
├── Supervised: Given correct action for each state
├── RL: Must discover correct actions through trial and error
├── RL more realistic for real-world problems
├── RL requires more samples but no labels needed
```

**Comparison of Learning Paradigms**:

```
| Aspect | Supervised | Unsupervised | Reinforcement |
|--------|-----------|-------------|--------------|
| Data Type | Labeled (x,y) | Unlabeled x | (s,a,r,s') tuples |
| Goal | Predict y from x | Discover patterns | Maximize reward |
| Feedback | Labels (explicit) | None (implicit) | Delayed rewards |
| Complexity | Low-Medium | High (discovery) | High (exploration) |
| Examples | Classification, Regression | Clustering, Dimensionality | Game playing, Robotics |
| Sample Efficiency | Moderate | High (less data) | Low (needs many trials) |
| Real-world | Diagnosis, spam detection | Data exploration | Robot control, Game AI |
```

---

## 2.2 Single Perceptron

### 2.2.1 Perceptron Fundamentals

**Definition**: Simplest neural network; single neuron classifier for linearly separable data.

```
Biological Inspiration:
├── Neuron: Receives signals, processes, outputs
├── Synapse: Connection with weight
├── Firing: Neuron activates if input exceeds threshold
└── Learning: Synapses strengthen/weaken

Artificial Perceptron Components:

    Inputs: x₁, x₂, ..., xₙ
       ↓
    Weights: w₁, w₂, ..., wₙ
       ↓
    Weighted Sum: net = Σ(wᵢ × xᵢ) + b
                      i=1
       ↓
    Activation Function: f(net)
       ↓
    Output: y ∈ {0,1} or {-1,1}
```

### 2.2.2 Perceptron Model

```
Mathematical Model:

Net Input:
net = Σ(wᵢ × xᵢ) + b = w^T × x + b

where:
├── w: Weight vector [w₁, w₂, ..., wₙ]
├── x: Input vector [x₁, x₂, ..., xₙ]
├── b: Bias term (threshold offset)
└── w^T × x: Dot product

Activation Function (Heaviside/Step):
        { 1    if net ≥ 0
f(net)={
        {-1    if net < 0

or alternatively:
        { 1    if net ≥ θ
f(net)={
        { 0    if net < θ

Output:
y = f(net) = f(w^T × x + b)

Geometric Interpretation:
├── Decision boundary: w^T × x + b = 0 (hyperplane)
├── Points on one side: Class 1
├── Points other side: Class -1
├── Perceptron finds separating hyperplane
└── Only works for linearly separable data
```

### 2.2.3 Perceptron Learning Rule

**Goal**: Find weights w and bias b that correctly classify all training examples.

```
Algorithm:

Initialize weights w randomly (or to zero)
Learning rate: η (small positive value, e.g., 0.1)

repeat until convergence:
    for each training example (x, y):
        Calculate output: ŷ = f(w^T × x + b)
        
        if ŷ ≠ y:  (Prediction error)
            Update weights: w ← w + η × y × x
            Update bias: b ← b + η × y
        
        else:  (Correct prediction)
            No change: w ← w, b ← b

until no errors or max iterations

Explanation:

When Error Occurs (ŷ ≠ y):
├── ŷ = 1 but y = -1 (false positive)
│   └── Reduce positive activation: w ← w - η × x
├── ŷ = -1 but y = 1 (false negative)
│   └── Increase positive activation: w ← w + η × x
└── Update moves decision boundary toward correct side

Update Rule Analysis:
├── η × y × x: Scaled input vector
├── Sign of y determines direction (add or subtract)
├── Magnitude of update determined by η
└── Repeated updates move boundary iteratively
```

### 2.2.4 Example: Perceptron for AND Function

```
Problem: Learn Boolean AND function

Inputs: x₁, x₂ ∈ {0, 1}
Output: y = x₁ AND x₂

Truth Table:
├── (0,0) → 0
├── (0,1) → 0
├── (1,0) → 0
└── (1,1) → 1

Linearly Separable? YES
Decision boundary needed: Separate (1,1) from others

Graphical Representation:
    x₂
    │  1 ├─────●(1,1) ← Class 1
    │    │   /
    │    │  / (decision boundary)
    │    │ /
    │  0 ●─────●────●  x₁
       (0,0) (1,0)
    Class -1

Perceptron Learning:

Initialize: w = [0, 0], b = 0, η = 0.1

Iteration 1:
Example 1: x=(0,0), y=-1
    net = 0×0 + 0×0 + 0 = 0
    ŷ = f(0) = 1 (ERROR: should be -1)
    Update: w ← [0,0] + 0.1×(-1)×[0,0] = [0,0]
            b ← 0 + 0.1×(-1) = -0.1

Example 2: x=(0,1), y=-1
    net = 0×0 + 0×1 + (-0.1) = -0.1
    ŷ = f(-0.1) = -1 (CORRECT)
    No update

Example 3: x=(1,0), y=-1
    net = 0×1 + 0×0 + (-0.1) = -0.1
    ŷ = f(-0.1) = -1 (CORRECT)
    No update

Example 4: x=(1,1), y=1
    net = 0×1 + 0×1 + (-0.1) = -0.1
    ŷ = f(-0.1) = -1 (ERROR: should be 1)
    Update: w ← [0,0] + 0.1×1×[1,1] = [0.1, 0.1]
            b ← -0.1 + 0.1×1 = 0

Iteration 2 (repeat with new weights):
Example 1: x=(0,0), y=-1
    net = 0.1×0 + 0.1×0 + 0 = 0
    ŷ = f(0) = 1 (ERROR)
    Update: w ← [0.1, 0.1] - 0.1×[0,0] = [0.1, 0.1]
            b ← 0 - 0.1 = -0.1

Example 2: x=(0,1), y=-1
    net = 0.1×0 + 0.1×1 - 0.1 = 0
    ŷ = f(0) = 1 (ERROR)
    Update: w ← [0.1, 0.1] - 0.1×[0,1] = [0.1, 0.0]
            b ← -0.1 - 0.1 = -0.2

... (continue iterations) ...

Final Weights (after convergence):
w ≈ [0.5, 0.5], b ≈ -0.3

Test:
├── (0,0): net = 0.5×0 + 0.5×0 - 0.3 = -0.3 → -1 ✓
├── (0,1): net = 0.5×0 + 0.5×1 - 0.3 = 0.2 → 1 ✗ (should be -1)
... (adjust parameters)

Final converged: w ≈ [0.6, 0.6], b ≈ -0.7
├── (0,0): net = -0.7 → -1 ✓
├── (0,1): net = 0.6 - 0.7 = -0.1 → -1 ✓
├── (1,0): net = 0.6 - 0.7 = -0.1 → -1 ✓
└── (1,1): net = 0.6 + 0.6 - 0.7 = 0.5 → 1 ✓
```

### 2.2.5 Perceptron Convergence Theorem

**Theorem Statement**:

```
If a training set is linearly separable (can be perfectly
classified by some hyperplane), the perceptron learning
algorithm is guaranteed to find a solution in finite number
of iterations.

Formal:

Given:
├── Training set D = {(x₁,y₁), (x₂,y₂), ..., (xₙ,yₙ)}
├── Data is linearly separable
├── ∃ weight vector w* and bias b* that perfectly classify D
└── Margin γ > 0 (minimum distance from data to separating hyperplane)

Then:
The perceptron algorithm terminates in at most R²/γ² iterations
where R is bound on input magnitudes

Implications:

Advantages:
├── Guaranteed convergence on separable data
├── Simple to implement and understand
├── Efficient: Linear time in data size
└── Theoretically sound

Limitations:
├── FAILS on non-separable data
├── Algorithm never terminates if data not separable
├── Oscillates without converging
├── No way to know if data separable beforehand
└── Single neuron can't learn XOR (not linearly separable)

Examples:

Linearly Separable (Perceptron works):
├── AND function: Decision boundary line separates classes
├── OR function: Decision boundary line separates classes
└── Converges to solution

NOT Linearly Separable (Perceptron fails):
├── XOR function:
│   ├── (0,0) → 0
│   ├── (0,1) → 1
│   ├── (1,0) → 1
│   └── (1,1) → 0
│   No single line separates the classes!
├── Concentric circles: Inner circle one class, outer ring other
└── Any dataset that spirals or interleaves
```

### 2.2.6 Perceptron Limitations

```
1. Linearly Separable Data Only:
   ├── Cannot learn non-linearly separable patterns
   ├── XOR requires multiple layers
   ├── Many real-world problems non-separable
   └── Single neuron limited expressiveness

2. Binary Classification Only:
   ├── Outputs {0,1} or {-1,1}
   ├── Cannot naturally handle multi-class
   ├── Requires one-vs-all approach for multiple classes
   └── Inefficient

3. No Probability Estimates:
   ├── Hard decisions only
   ├── No confidence in predictions
   ├── Cannot express uncertainty
   └── Sigmoid/softmax needed for probabilities

4. Inefficient on Large Datasets:
   ├── Slow convergence if data nearly non-separable
   ├── One mistake per update (could be inefficient)
   └── No batch learning possible

5. Parameter Sensitivity:
   ├── Learning rate η affects convergence speed
   ├── Too high: Overshooting
   ├── Too low: Slow convergence
   └── No principled way to set η

Solution: Multi-Layer Perceptron (MLP) / Neural Networks
```

---

## 2.3 Multi-Layer Perceptron

### 2.3.1 MLP Architecture

**Motivation**: Single perceptron limited to linearly separable problems. MLPs solve this with multiple layers.

```
Network Structure:

Input Layer:
├── n neurons (inputs)
├── One neuron per feature
└── No processing (just pass through)

Hidden Layer(s):
├── Multiple layers of neurons
├── Nonlinear activation functions
├── Transform input space
└── Extract features

Output Layer:
├── Output neurons (depends on task)
├── Classification: K neurons (K classes)
├── Regression: 1 neuron
└── Activation: Task-dependent

Example: 3-Layer Network (2 hidden layers)

Inputs → Hidden1 → Hidden2 → Outputs

    x₁        h₁¹    h₁²          ŷ₁
    x₂        h₂¹    h₂²          ŷ₂
    x₃ ──────────────────────────
    x₄        h₃¹    h₃²
              h₄¹    h₂²
                     h₃²

Connections:
├── Input to Hidden1: fully connected
├── Hidden1 to Hidden2: fully connected
├── Hidden2 to Output: fully connected

Parameters:
├── Input layer: n neurons
├── Hidden layer 1: 4 neurons
├── Hidden layer 2: 3 neurons
├── Output layer: 2 neurons
├── Weights: n×4 + 4×3 + 3×2 = 4n + 18
└── Plus biases: 4 + 3 + 2 = 9
```

### 2.3.2 Activation Functions

**Why Activation Functions?**

```
Without activation:
├── Output = w₃×(w₂×(w₁×x)) = (w₃w₂w₁)×x
├── Still linear combination of inputs
├── Multi-layer reduces to single layer
├── Cannot represent nonlinear functions

With activation:
├── Introduce nonlinearity
├── Each layer nonlinear
├── Layers compose: nonlinear ∘ nonlinear = more nonlinear
├── Can approximate any function (Universal Approximation)
```

**Common Activation Functions**:

```
1. Sigmoid (Logistic)

Definition:
σ(z) = 1 / (1 + e^(-z))

Range: (0, 1)
Properties:
├── Smooth, differentiable
├── S-shaped curve
├── Historical: First used
├── Output interpretable as probability
└── Derivative: σ'(z) = σ(z) × (1 - σ(z))

Graph:
    1.0 ├──────────────┐
        │              /
   0.75 │            ╱
        │          ╱
   0.5  │    ─────╱─────
        │  ╱
   0.25 │ ╱
        │/
    0.0 └──────────────
      -5 0 5

Issues:
├── Vanishing gradient: derivative small for |z| large
├── Slower training in deep networks
├── Kills gradients in early layers
└── Saturates (output near 0 or 1)

Usage:
├── Output layer for binary classification
├── Historically popular but less common now
└── Still used in recurrent networks
```

```
2. Tanh (Hyperbolic Tangent)

Definition:
tanh(z) = (e^z - e^(-z)) / (e^z + e^(-z)) = 2σ(2z) - 1

Range: (-1, 1)
Properties:
├── Similar shape to sigmoid
├── Centered at 0 (better than sigmoid)
├── Stronger gradients than sigmoid
└── Derivative: tanh'(z) = 1 - tanh²(z)

Graph:
    1.0 ├──────────────┐
        │            ╱
   0.5  │          ╱
        │        ╱
    0.0 ├──────╱─────── (centered)
        │    ╱
  -0.5  │  ╱
        │╱
   -1.0 └──────────────
      -5 0 5

Advantages over Sigmoid:
├── Centered (symmetric around 0)
├── Slightly better gradient flow
├── Often faster convergence
└── Generally preferred

Usage:
├── Hidden layers in traditional networks
├── Recurrent neural networks
└── When symmetric output preferred
```

```
3. ReLU (Rectified Linear Unit)

Definition:
ReLU(z) = max(0, z)

Range: [0, ∞)
Properties:
├── Simple: Just threshold at 0
├── Fast to compute
├── Non-zero for positive inputs
├── Zero for negative inputs
└── Derivative: 1 if z > 0, else 0

Graph:
        │    ╱
    y   │  ╱
        │╱ (goes through origin)
    ────┼─────── z
        │

Advantages:
├── Solves vanishing gradient (linear for z>0)
├── Faster training (simple computation)
├── Sparsity (many units output 0)
└── Works well in deep networks

Issues:
├── Dead ReLU: Neuron outputs 0 forever if never activated
├── Cannot output negative values
├── Non-differentiable at 0 (but not critical)
└── Can have high variance

Usage:
├── Most common in hidden layers
├── Default choice for deep networks
├── Standard in modern architectures
└── Variants: Leaky ReLU, ELU, etc.

Leaky ReLU (Variant):

Definition:
LeakyReLU(z) = max(αz, z) where α ≈ 0.01

Advantage:
├── Prevents dead ReLU problem
├── Allows small negative values
├── Better gradient flow
└── α is learnable in some variants

Graph:
        │   ╱
        │ ╱
    ────┼─────── (small slope for z<0)
        │ α×z
        ├ (slope α, not 0)
```

```
4. Softmax

Definition:
softmax(z)ᵢ = e^zᵢ / Σⱼ(e^zⱼ)

Used for: Multi-class classification output layer

Properties:
├── Converts outputs to probabilities
├── Sums to 1: Σ softmax(z) = 1
├── Differentiable
└── One-hot encoded outputs

Example:
Input: z = [2.0, 1.0, 0.1]

e^z = [e², e¹, e^0.1] ≈ [7.39, 2.72, 1.10]
Sum = 11.21

softmax(z) ≈ [0.659, 0.243, 0.098]
(~66% class 1, ~24% class 2, ~10% class 3)

Properties:
├── Output as probability distribution
├── Good for classification
├── Differentiable for backprop
└── Standard output layer for multi-class

Usage:
├── Output layer for multi-class classification
├── Always paired with cross-entropy loss
└── Prevents outputs > 1 or negative
```

```
5. Linear (Identity)

Definition:
linear(z) = z

Properties:
├── No activation (identity function)
├── Preserves input
├── Full range: (-∞, ∞)
└── Derivative = 1

Usage:
├── Output layer for regression
├── Rarely in hidden layers (same as no activation)
└── Important for continuous outputs
```

### 2.3.3 Forward Propagation

**Process**: Computing output by passing input through network.

```
Network Example:
    Input Layer (2 neurons)
         ↓ (weights w¹)
    Hidden Layer (3 neurons)
         ↓ (weights w²)
    Output Layer (1 neuron)

Notation:
├── Layer l: neurons numbered 1 to nₗ
├── w^(l): Weights from layer l-1 to layer l
├── b^(l): Bias for layer l
├── z^(l): Pre-activation (before activation function)
├── a^(l): Post-activation (after activation function)
└── a^(0) = x (inputs)

Forward Pass Algorithm:

Input: x (input vector)

Layer 1 (input to hidden):
    z¹ᵢ = Σⱼ(w¹ᵢⱼ × xⱼ) + b¹ᵢ           (pre-activation)
    a¹ᵢ = σ(z¹ᵢ)                        (post-activation, using ReLU typically)

Layer 2 (hidden to output):
    z²ᵢ = Σⱼ(w²ᵢⱼ × a¹ⱼ) + b²ᵢ          (pre-activation)
    a²ᵢ = σ(z²ᵢ) or linear(z²ᵢ)         (post-activation)

Output: a² (final layer output)

Example Calculation:

Network:
    x₁ ─w¹₁₁→ h₁ ─w²₁₁→ ŷ
    x₂ ─w¹₁₂→ ├─ w²₁₂→ └─
          ...
          h₃ ─w²₁₃→

Given:
├── Inputs: x = [2, 3]
├── Layer 1 weights: w¹ = [[0.5, 0.3], [0.2, 0.4], [0.1, 0.5]]
├── Layer 1 biases: b¹ = [0.1, 0.2, 0.3]
├── Layer 2 weights: w² = [[0.6, 0.8, 0.4]]
├── Layer 2 bias: b² = [0.2]
└── Activation: ReLU for hidden, linear for output

Step 1: Pre-activations (Layer 1)
    z¹₁ = 0.5×2 + 0.3×3 + 0.1 = 1.0 + 0.9 + 0.1 = 2.0
    z¹₂ = 0.2×2 + 0.4×3 + 0.2 = 0.4 + 1.2 + 0.2 = 1.8
    z¹₃ = 0.1×2 + 0.5×3 + 0.3 = 0.2 + 1.5 + 0.3 = 2.0

Step 2: Activations (Layer 1, ReLU)
    a¹₁ = max(0, 2.0) = 2.0
    a¹₂ = max(0, 1.8) = 1.8
    a¹₃ = max(0, 2.0) = 2.0

Step 3: Pre-activations (Layer 2)
    z² = 0.6×2.0 + 0.8×1.8 + 0.4×2.0 + 0.2
       = 1.2 + 1.44 + 0.8 + 0.2
       = 3.64

Step 4: Activation (Layer 2, linear)
    a² = 3.64

Output: ŷ = 3.64

Matrix Form (More Efficient):

z^(l) = w^(l) @ a^(l-1) + b^(l)         (@ is matrix multiply)
a^(l) = σ(z^(l))

Example in matrix form:
z¹ = w¹ @ x + b¹ = [[0.5, 0.3], ...] @ [[2], [3]] + [[0.1], ...]
   = [[1.0], [0.4], [0.2]] + [[0.1], [0.2], [0.3]]
   = [[2.0], [1.8], [2.0]]
```

### 2.3.4 Backpropagation Algorithm

**Purpose**: Compute gradients of loss with respect to weights for updating.

#### 1.3.4.1 Core Concept

```
Chain Rule:
∂L/∂w = (∂L/∂z) × (∂z/∂w)

For network:
w → z → a → L (loss)

∂L/∂w = (∂L/∂a) × (∂a/∂z) × (∂z/∂w)

Key Insight:
├── Forward pass: Compute z, a
├── Backward pass: Compute gradients backward
├── Use intermediate values from forward
└── Efficient: Don't recompute (O(n) instead of O(n²))
```

#### 2.3.4.2 Backpropagation Algorithm

```
Algorithm: Backpropagation through MLP

Step 1: Forward Pass (compute activations)
    for l = 1 to L:  (L = number of layers)
        z^(l) = w^(l) @ a^(l-1) + b^(l)
        a^(l) = σ(z^(l))

Step 2: Compute Output Error
    δ^(L) = ∇_a L ⊙ σ'(z^(L))
    
    where:
    ├── ∇_a L = (a^(L) - y) for MSE loss
    ├── (a^(L) - y) = predicted - actual
    ├── σ'(z^(L)) = derivative of activation
    ├── ⊙ = element-wise multiplication
    └── δ = "error" for layer

Step 3: Backward Pass (propagate error)
    for l = L-1 down to 1:
        δ^(l) = (w^(l+1)^T @ δ^(l+1)) ⊙ σ'(z^(l))
        
    Interpretation:
    ├── w^(l+1)^T @ δ^(l+1) = error from next layer
    ├── "Blame" current layer for next layer's error
    ├── Scale by activation derivative
    └── Propagate backward through layers

Step 4: Compute Weight Gradients
    for l = 1 to L:
        ∂L/∂w^(l) = δ^(l) @ a^(l-1)^T
        ∂L/∂b^(l) = δ^(l)

Step 5: Update Weights (Gradient Descent)
    for l = 1 to L:
        w^(l) ← w^(l) - α × ∂L/∂w^(l)
        b^(l) ← b^(l) - α × ∂L/∂b^(l)
    
    where:
    ├── α = learning rate
    └── Update opposite to gradient (descent)

Pseudocode:

```
function backpropagation(x, y, network, α):
    // Forward pass
    a^(0) = x
    for l = 1 to L:
        z^(l) = w^(l) @ a^(l-1) + b^(l)
        a^(l) = activation(z^(l))
    
    // Output error
    δ^(L) = (a^(L) - y) * activation_derivative(z^(L))
    
    // Backward pass
    for l = L-1 down to 1:
        δ^(l) = (w^(l+1)^T @ δ^(l+1)) * activation_derivative(z^(l))
    
    // Compute gradients
    for l = 1 to L:
        dw^(l) = δ^(l) @ a^(l-1)^T
        db^(l) = δ^(l)
    
    // Update weights
    for l = 1 to L:
        w^(l) = w^(l) - α * dw^(l)
        b^(l) = b^(l) - α * db^(l)
    
    return network
```

Computational Complexity:
├── Forward: O(total_weights) 
├── Backward: O(total_weights)
├── Total: O(weights) = efficient
└── Batch operations: Vectorized (GPU friendly)
```

#### 2.3.4.3 Backpropagation Example

```
Simple 2-layer network training on one example

Network:
    x₁ → h₁ → ŷ
    x₂ → 
        h₂

Layer 1: 2→2 (input to hidden)
├── w¹ = [[0.5, 0.3], [0.2, 0.4]]
└── b¹ = [[0.1], [0.2]]

Layer 2: 2→1 (hidden to output)
├── w² = [[0.6, 0.8]]
└── b² = [0.1]

Training example: x = [[2], [3]], y = [0.5]
Learning rate: α = 0.1
Activation: ReLU for hidden, linear for output

FORWARD PASS:

Layer 1:
z¹ = w¹ @ x + b¹ = [[0.5, 0.3], [0.2, 0.4]] @ [[2], [3]] + [[0.1], [0.2]]
   = [[1.0], [0.4]] + [[0.1], [0.2]] = [[2.0], [1.8]]
   
a¹ = ReLU(z¹) = [[2.0], [1.8]]  (both positive, no change)

Layer 2:
z² = w² @ a¹ + b² = [[0.6, 0.8]] @ [[2.0], [1.8]] + [0.1]
   = [1.2 + 1.44] + [0.1] = [2.74]
   
a² = linear(z²) = [2.74]

Prediction: ŷ = 2.74

BACKWARD PASS:

Output error:
δ² = (a² - y) × linear'(z²) = (2.74 - 0.5) × 1 = [2.24]

Hidden layer error:
δ¹ = (w²^T @ δ²) ⊙ ReLU'(z¹)
   = ([[0.6], [0.8]] @ [2.24]) ⊙ [[1], [1]]  (ReLU' = 1 for z>0)
   = [[0.6×2.24], [0.8×2.24]] ⊙ [[1], [1]]
   = [[1.344], [1.792]] ⊙ [[1], [1]]
   = [[1.344], [1.792]]

GRADIENT COMPUTATION:

dw²/dL = δ² @ a¹^T = [2.24] @ [[2.0, 1.8]]
       = [[2.24×2.0, 2.24×1.8]] = [[4.48, 4.032]]

db²/dL = δ² = [2.24]

dw¹/dL = δ¹ @ x^T = [[1.344], [1.792]] @ [[2, 3]]
       = [[1.344×2, 1.344×3], [1.792×2, 1.792×3]]
       = [[2.688, 4.032], [3.584, 5.376]]

db¹/dL = δ¹ = [[1.344], [1.792]]

WEIGHT UPDATE:

w² ← w² - α × dw² = [[0.6, 0.8]] - 0.1 × [[4.48, 4.032]]
   = [[0.6 - 0.448, 0.8 - 0.4032]]
   = [[0.152, 0.3968]]

b² ← b² - α × db² = [0.1] - 0.1 × [2.24]
   = [0.1 - 0.224] = [-0.124]

w¹ ← w¹ - α × dw¹ = [[0.5, 0.3], [0.2, 0.4]] - 0.1 × [[2.688, 4.032], [3.584, 5.376]]
   = [[0.5-0.2688, 0.3-0.4032], [0.2-0.3584, 0.4-0.5376]]
   = [[0.2312, -0.1032], [-0.1584, -0.1376]]

b¹ ← b¹ - α × db¹ = [[0.1], [0.2]] - 0.1 × [[1.344], [1.792]]
   = [[0.1-0.1344], [0.2-0.1792]]
   = [[-0.0344], [0.0208]]

RESULT:

Loss changed from: (2.74-0.5)² = 5.0176 (before)

After one iteration, run forward again with new weights:
(Loss will be reduced)

Repeat until convergence
```

### 2.3.5 Training MLP Networks

```
Training Process:

1. Initialization:
   ├── Random weight initialization (small values)
   ├── Biases usually 0
   └── Important: Small random prevents symmetry

2. Hyperparameter Selection:
   ├── Learning rate α
   ├── Number of hidden layers
   ├── Neurons per layer
   ├── Activation functions
   ├── Batch size (for mini-batch gradient descent)
   └── Number of epochs

3. Training Loop:
   for epoch = 1 to max_epochs:
       for batch in training_data:
           1. Forward pass: Compute predictions
           2. Compute loss: L = (1/n) Σ(y - ŷ)²
           3. Backward pass: Compute gradients
           4. Update weights: w ← w - α × ∇L
       
       Validate on validation set
       if no improvement for patience iterations:
           Early stopping (stop training)

4. Optimization Variants:

   Stochastic Gradient Descent (SGD):
   ├── Update after each sample
   ├── Fast but noisy
   └── Can escape local minima

   Mini-batch SGD (most common):
   ├── Update after batch (e.g., 32 samples)
   ├── Balance between SGD and Batch
   ├── Stable and efficient
   └── GPU-friendly (vectorized)

   Adam Optimizer:
   ├── Adaptive learning rates
   ├── Momentum term
   ├── Works well in practice
   └── Less tuning needed

5. Convergence Monitoring:
   ├── Training loss: Should decrease
   ├── Validation loss: Should decrease
   ├── Gap between train/val: Indicates overfitting
   ├── Early stopping: Stop if validation not improving
   └── Learning curves: Plot loss vs epochs

6. Regularization (Prevent Overfitting):
   ├── L1/L2 regularization: Add penalty on weights
   ├── Dropout: Randomly disable neurons during training
   ├── Batch normalization: Normalize layer inputs
   ├── Early stopping: Stop before overtraining
   └── Data augmentation: Generate more training data
```

---

## 2.4 Self-Organizing Maps

### 2.4.1 SOM Fundamentals

**Definition**: Unsupervised neural network that maps high-dimensional input data onto 2D grid of neurons, preserving topological structure.

**Key Characteristics**:

```
1. Topology:
   ├── Neurons organized in 2D grid (usually)
   ├── Usually square: N×N grid
   ├── Neighbor relationships defined by grid position
   └── Distant neurons: Dissimilar inputs

2. Unsupervised Learning:
   ├── No labels needed
   ├── Discovers inherent structure
   ├── Competitive learning
   └── Self-organization

3. Dimensionality Reduction:
   ├── High-dimensional input → 2D grid
   ├── Preserves relationships
   ├── Enables visualization
   └── Clusters emerge naturally

4. Topology Preservation:
   ├── Similar inputs activate nearby neurons
   ├── Topological ordering maintained
   ├── Geodesic distances related
   └── Manifold structure captured

Visual representation:

Input Space (e.g., 10D)          SOM Grid (2D)
┌─────────────────────┐         ┌─────────────────┐
│  ● ●                │         │ ① ② ③ ④ ⑤      │
│    ● ●              │    →    │ ⑥ ⑦ ⑧ ⑨ ⑩     │
│  ●     ●            │         │ ⑪ ⑫ ⑬ ⑭ ⑮     │
│      ●              │         │ ⑯ ⑰ ⑱ ⑲ ⑳     │
│        ●  ●  ●      │         └─────────────────┘
└─────────────────────┘

High-dim structure        2D visualization
preserved in 2D          easy to interpret
```

### 2.4.2 SOM Architecture

```
Components:

1. Input Layer:
   ├── n neurons (one per input dimension)
   ├── No processing
   └── Pass through inputs

2. Competitive Layer (SOM Layer):
   ├── 2D grid of neurons (N×N)
   ├── Each neuron i has weight vector w^i ∈ ℝⁿ
   ├── Weight vector same dimensionality as input
   └── Usually randomly initialized

3. Connections:
   ├── Input to SOM: Fully connected
   ├── Each input connected to all SOM neurons
   ├── SOM neurons: Local connections (neighbors)
   └── Weight updates proportional to distance

Network Visualization:

                    Input Vector x
                    (10-dimensional)
                          │
        ┌─────────────────┼─────────────────┐
        ↓    ↓    ↓    ↓    ↓    ↓    ↓    ↓
    [w¹] [w²] [w³] [w⁴] [w⁵] [w⁶] [w⁷] [w⁸]
     (each wⁱ is 10-D vector)
     
    Forming a 2×4 SOM:
    ┌───┬───┬───┬───┐
    │ 1 │ 2 │ 3 │ 4 │
    ├───┼───┼───┼───┤
    │ 5 │ 6 │ 7 │ 8 │
    └───┴───┴───┴───┘
    
    (neuron 6 neighbors: 2, 5, 7, 10)
```

### 2.4.3 SOM Learning Algorithm

**Core Process**: Kohonen Learning Rule

```
1. INITIALIZATION:

   Initialize SOM grid (N×N neurons)
   For each neuron i:
       w^i = random vector in input space
       
   Set learning rate: α(t)  (decreases over time)
   Set neighborhood size: σ(t) (decreases over time)

2. COMPETITION:

   For each input sample x:
       Calculate distance to each neuron
       d_i = ||x - w^i||  (usually Euclidean)
       
       Find Best Matching Unit (BMU):
       c = argmin_i(d_i)  (neuron closest to input)

3. COOPERATION:

   Calculate neighborhood function:
   h_{c,i}(t) = exp(-||r_c - r_i||² / (2σ(t)²))
   
   where:
   ├── r_c: position of BMU in grid
   ├── r_i: position of neuron i in grid
   ├── σ(t): neighborhood radius (decreases with time)
   └── h: larger for nearby neurons, smaller for distant

4. ADAPTATION (LEARNING):

   Update all neurons:
   w^i(t+1) = w^i(t) + α(t) × h_{c,i}(t) × (x - w^i(t))
   
   where:
   ├── α(t): Learning rate (typically 0.1 to 0.5, decreases)
   ├── h_{c,i}(t): Neighborhood influence
   ├── (x - w^i(t)): Direction to move toward input
   └── Update proportional to neighborhood

Pseudocode:

```
function SOM_train(data, grid_size, epochs):
    N = grid_size  // e.g., 10×10
    n_dim = dimension of input
    
    // Initialization
    SOM = initialize_random_grid(N, N, n_dim)
    
    for epoch = 1 to epochs:
        α(epoch) = α_initial × exp(-epoch / time_constant)
        σ(epoch) = σ_initial × exp(-epoch / time_constant)
        
        shuffle(data)
        for each input sample x in data:
            // Competition
            bmu = find_bmu(x, SOM)  // best matching unit
            
            // Adaptation
            for each neuron i in SOM:
                distance = grid_distance(i, bmu)
                h = neighborhood_function(distance, σ(epoch))
                SOM[i] = SOM[i] + α(epoch) × h × (x - SOM[i])
    
    return SOM
```

### 2.4.4 SOM Example

```
Problem: Cluster 2D data points into organized map

Data: 100 points scattered in 2D
Target: 3×3 SOM grid (9 neurons)

Initial State:
├── Neurons randomly placed in 2D space
├── No structure
└── Uniform coverage

Input Data (example):
  Points cluster in 3 regions:
  ├── Top-left cluster
  ├── Center-top cluster
  └── Bottom-right cluster

Training Process:

Epoch 1:
├── Learning rate α = 0.5
├── Neighborhood σ = 1.5
├── Few neurons activated for each input
├── Coarse organization begins

Epoch 10:
├── Learning rate α = 0.3
├── Neighborhood σ = 1.0
├── More refined organization
├── Clusters starting to separate

Epoch 50:
├── Learning rate α = 0.1
├── Neighborhood σ = 0.5
├── Fine-tuned organization
├── Clear topological structure

Final Result:
    ┌────────────────────────┐
    │  * *    * *    * *    │
    │    *  ●    *  ●    *  │  * = data points
    │  * *    * *    * *    │  ● = neuron
    │                       │
    │  * *    * *    * *    │
    │    *  ●    *  ●    *  │
    │  * *    * *    * *    │
    │                       │
    │  * *    * *    * *    │
    │    *  ●    *  ●    *  │
    │  * *    * *    * *    │
    └────────────────────────┘

Each neuron surrounded by similar inputs
Topological ordering: Adjacent neurons similar inputs
```

### 2.4.5 SOM Applications and Properties

```
Applications:

1. Data Clustering and Visualization:
   ├── Visualize high-dimensional data
   ├── Discover natural clusters
   ├── Explore data structure
   └── Identify relationships

2. Feature Extraction:
   ├── Reduce dimensionality
   ├── Extract meaningful features
   ├── Compress data
   └── Preparation for other models

3. Pattern Recognition:
   ├── Speech recognition
   ├── Image classification
   ├── Text mining
   └── Bioinformatics

4. Quality Prediction:
   ├── Unsupervised clustering
   ├── Anomaly detection
   ├── Fault diagnosis
   └── Quality assessment

Advantages:

1. Topology Preservation:
   ├── Similar inputs cluster together
   ├── Topological relationships preserved
   └── Intuitive visualization

2. Unsupervised Learning:
   ├── No labels required
   ├── Discovers structure automatically
   ├── Flexible and exploratory
   └── Good for data understanding

3. Scalability:
   ├── Works with high-dimensional data
   ├── Can handle hundreds of dimensions
   ├── Efficient computation
   └── Easy to implement

4. Interpretability:
   ├── Visual representation
   ├── Easy to understand clusters
   ├── Domain expert friendly
   └── Good for storytelling

Limitations:

1. Fixed Architecture:
   ├── Grid size must be specified
   ├── Affects cluster count
   ├── Not automatic
   └── Requires trial and error

2. Computational Complexity:
   ├── O(n×m×k) per epoch (n samples, m neurons, k dimensions)
   ├── Can be slow for large datasets
   ├── Serial training (limited parallelization)
   └── Might need preprocessing

3. Local Minima:
   ├── Solution depends on initialization
   ├── Different runs may give different results
   ├── No global optimality guarantee
   └── May need multiple runs

4. Parameter Tuning:
   ├── Learning rate decay function
   ├── Neighborhood function
   ├── Grid size and topology
   ├── Convergence criteria
   └── Multiple parameters to tune
```

---

## 2.5 Hopfield Networks

### 2.5.1 Hopfield Network Fundamentals

**Definition**: Recurrent neural network that acts as associative memory; stores patterns and retrieves them even from partial/noisy input.

```
Key Characteristics:

1. Recurrent:
   ├── Neurons connected in feedback loops
   ├── Output feeds back to input
   ├── Dynamic system with temporal evolution
   └── States change over time

2. Fully Connected:
   ├── Every neuron connected to every other
   ├── Bidirectional: i↔j weight = j↔i weight (symmetric)
   ├── No self-connections: w_{ii} = 0
   └── All-to-all connectivity

3. Associative Memory:
   ├── Store patterns during training
   ├── Retrieve patterns from partial input
   ├── Robustness to noise
   ├── Content-addressable memory (CAM)
   └── Pattern completion

4. Energy Function:
   ├── Network has associated energy
   ├── Updates minimize energy
   ├── Converges to local minima
   ├── Minima correspond to stored patterns
   └── Energy landscape governs dynamics

Visual Structure:

Network Diagram (4 neurons):
    ┌─────────────────────┐
    │    w₁₂    w₁₃       │
    ├────┴────┬────┴───┬──┤
    ↓         ↓        ↓  ↓
    1●────────2●       3● 4●
       w₂₁  ╱  w₂₃    ╱
         ╱      ╱    ╱
         ───────────
    
Connections:
├── Neuron 1 to others: 1→2, 1→3, 1→4
├── Neuron 2 to others: 2→1, 2→3, 2→4
├── Symmetric: w_{ij} = w_{ji}
└── All neurons interact
```

### 2.5.2 Hopfield Network Model

```
Components:

1. Neurons:
   ├── Binary: yᵢ ∈ {0, 1} or {-1, 1}
   ├── Threshold: θᵢ
   └── Activation: Update rule (synchronous or asynchronous)

2. Weights:
   ├── w_{ij}: Connection strength i to j
   ├── Symmetric: w_{ij} = w_{ji}
   ├── No self-loops: w_{ii} = 0
   └── Can be positive (excitatory) or negative (inhibitory)

3. Dynamics:

   Net input to neuron i:
   xᵢ = Σⱼ(w_{ij} × yⱼ) - θᵢ

   Update rule (threshold):
       { 1      if xᵢ ≥ 0
   yᵢ={
       {-1      if xᵢ < 0

   or for binary:
       { 1      if xᵢ ≥ θᵢ
   yᵢ={
       { 0      if xᵢ < θᵢ

4. Energy Function:

   E = -½ Σᵢ Σⱼ(w_{ij} × yᵢ × yⱼ) + Σᵢ(θᵢ × yᵢ)

   Properties:
   ├── Decreases with each update
   ├── Bounded below (minimum exists)
   ├── Converges to local minimum
   ├── Minima = stable states = stored patterns
   └── Lyapunov function
```

### 2.5.3 Hopfield Learning Rule (Hebb's Rule)

**Objective**: Store patterns in weight matrix

```
Given patterns to store: {p¹, p², ..., pᵐ}
Each pattern pᵏ = [p¹ₖ, p²ₖ, ..., pⁿₖ] is n-dimensional binary vector

Hebbian Learning Rule:

For pattern p:
w_{ij} = Σ_{over all patterns}(pᵢ × pⱼ)

Simplified for single pattern p:
w_{ij} = pᵢ × pⱼ  (if i ≠ j)
w_{ii} = 0

Matrix Form:
W = p × p^T - I  (for single pattern)

where:
├── p: Pattern vector (column)
├── p^T: Pattern transpose (row)
├── p × p^T: Outer product (n×n matrix)
└── I: Identity matrix (diagonal = 1)

For Multiple Patterns:
W = Σₖ(pᵏ × (pᵏ)^T) - m×I

where m = number of patterns

Example:

Pattern to store: p = [1, -1, 1, -1]^T

Outer product p × p^T:
       [ 1]           [ 1  -1   1  -1]
       [-1]  ×  [1 -1 1 -1] = [-1  1  -1  1]
       [ 1]           [ 1  -1   1  -1]
       [-1]           [-1  1   -1  1]

Weight matrix (after removing diagonal):
       [ 0  -1  1  -1]
   W = [-1  0  -1  1]
       [ 1  -1  0  -1]
       [-1  1  -1  0]

Interpretation:
├── w_{12} = -1: Neurons 1,2 should opposite (1,1 → -1)
├── w_{13} = 1: Neurons 1,3 should same (1,3 → same)
├── Weights encode pattern correlations
└── Retrieval amplifies pattern
```

### 2.5.4 Pattern Retrieval

```
Process: Recover stored pattern from partial/noisy input

Step 1: Initialize network with partial pattern
├── Set neuron states to input pattern
├── Missing values: Random or neutral (0)
├── Noisy values: Start with noisy version
└── Stored pattern encoded in weights

Step 2: Iterate Until Convergence
for iteration = 1 to max:
    for each neuron i (random order, asynchronous):
        xᵢ = Σⱼ(w_{ij} × yⱼ) - θᵢ
        
        if xᵢ ≥ 0:  yᵢ ← 1
        else:       yᵢ ← -1
        
        if no states changed in iteration:
            Convergence reached

Step 3: Return Final State
├── Final state = retrieved pattern
├── Should match one of stored patterns
├── Energy at local minimum
└── Pattern reconstruction complete

Example: Binary Image Retrieval

Stored Pattern (8 neurons representing 2×4 image):
Stored: p = [1, 1, 1, 1, -1, -1, -1, -1]
        ╔═══════╗
        ║ ■ ■ ■ ║ (stored pattern)
        ║ ░ ░ ░ ║
        ╚═════ ╝

Cue (60% corrupted):
Noisy: i = [1, -1, 1, -1, -1, 1, -1, -1]
       ╔═══════╗
       ║ ■ ░ ■ ║ (partial/noisy input)
       ║ ░ ■ ░ ║
       ╚═════ ╝

Iteration 1:
├── Neuron activities update
├── Weights push toward stored pattern
├── Some correct, some flip
└── Energy decreases

Iteration 2:
├── More neurons correct
├── Pattern becomes clearer
└── Further energy decrease

Final (converged):
Retrieved: [1, 1, 1, 1, -1, -1, -1, -1]
          ╔═══════╗
          ║ ■ ■ ■ ║ (fully recovered!)
          ║ ░ ░ ░ ║
          ╚═════ ╝

Successfully recovered despite noise!
```

### 2.5.5 Properties and Limitations

```
Positive Properties:

1. Associative Memory:
   ├── Content-addressable retrieval
   ├── Robustness to noise
   ├── Partial pattern retrieval
   └── Biologically plausible

2. Stable Convergence:
   ├── Energy function guarantees convergence
   ├── Always reaches stable state
   ├── No oscillation/chaos
   └── Deterministic dynamics

3. Learning is Simple:
   ├── Hebbian rule easy to implement
   ├── One-shot learning possible
   ├── No backpropagation needed
   └── Fast training

4. Parallel Processing:
   ├── Can update neurons in parallel
   ├── Distributed computation
   ├── Biological inspiration
   └── Hardware-friendly

Limitations:

1. Storage Capacity:
   ├── Can store ~0.15n patterns (n = network size)
   ├── Less than 0.15n: Reliable
   ├── More than 0.15n: Crosstalk, errors
   ├── Limited by network size
   └── Grows slowly with neurons

2. Spurious Attractors:
   ├── May converge to false patterns
   ├── Not all minima = original patterns
   ├── Combinations of patterns
   ├── Unintended memories
   └── Reduces reliability

3. Synchronization Issues:
   ├── Asynchronous: Works well, guaranteed convergence
   ├── Synchronous: May oscillate
   ├── Temporal dynamics complex
   └── May get stuck locally

4. Capacity vs. Reliability:
   ├── Can't pack too many patterns
   ├── More patterns → Cross-talk
   ├── Trade-off: Capacity vs. accuracy
   └── Not suitable for large-scale tasks

5. Limited Applications:
   ├── Works for binary patterns
   ├── Fixed-size patterns only
   ├── Fully connected architecture
   ├── Not suitable for complex tasks
   └── Modern alternatives often better

Comparison with Modern Approaches:

| Aspect | Hopfield | Modern Neural Networks |
|--------|----------|----------------------|
| Memory | Associative, implicit | Explicit, parametric |
| Learning | Fast (Hebbian) | Slower (backprop) |
| Capacity | Limited (~0.15n) | High (millions params) |
| Performance | Good for small patterns | Scales to complex tasks |
| Stability | Guaranteed convergence | No guarantees |
| Scalability | Poor (fully connected) | Excellent (sparse) |
| Training | One-shot | Iterative, tuning-heavy |

Modern Use:

Hopfield networks less common now:
├── Replaced by LSTMs/GRUs for temporal (recurrent)
├── Replaced by GANs for generative tasks
├── Replaced by Autoencoders for memory
├── Still used in:
│   ├── Optimization problems
│   ├── Image restoration
│   ├── Theoretical studies
│   └── Biologically-inspired models
└── Useful for understanding principles
```

---

# CONCLUSION

Unit III covers two fundamental areas of AI:

## Key Takeaways - Genetic Algorithms:

1. **Encoding**: Problem representation in chromosomes is critical (binary, real, permutation, value, tree)

2. **Operators**: Selection, crossover, mutation balance exploration/exploitation

3. **Fitness**: Well-designed fitness function guides evolution toward solutions

4. **GA Cycle**: Iterative process of selection, recombination, mutation, replacement

5. **Applications**: Optimization, scheduling, design, machine learning - any problem where solution can be encoded

6. **Stochasticity**: Randomness aids escaping local optima but requires multiple runs

## Key Takeaways - Neural Networks:

1. **Learning Paradigms**: Supervised (labeled), unsupervised (pattern discovery), reinforcement (reward-based)

2. **Perceptron**: Limited to linearly separable data but foundational concept

3. **MLP/Backpropagation**: Overcome perceptron limitations; enable training deep networks

4. **Activation Functions**: Nonlinearity essential for expressiveness (ReLU, sigmoid, tanh)

5. **SOM**: Unsupervised topology-preserving mapping for visualization and clustering

6. **Hopfield**: Associative memory with guaranteed convergence but limited capacity

7. **Scalability**: Modern deep networks far exceed simple architectures in capability

Both GAs and ANNs are powerful but different:
- **GA**: Stochastic search, works without gradient information, good for discrete problems
- **NN**: Gradient-based learning, backpropagation, excels with large continuous data
- **Combined**: Can use GA to optimize NN architecture/hyperparameters

---

# REFERENCES

**Primary Textbooks:**
1. Dan W. Patterson, "Introduction to Artificial Intelligence and Expert Systems" (Prentice-Hall, India)
2. David E. Goldberg, "Genetic Algorithms in Search, Optimization & Machine Learning" (Addison-Wesley)
3. S. Haykin, "Neural Networks and Learning Machines" (Pearson)

**Reference Materials:**
1. P. H. Winston, "Artificial Intelligence" (Addison Wesley)
2. A. Rich and K. Knight, "Artificial Intelligence" (Tate McGraw Hill)
3. N. J. Nilsson, "Artificial Intelligence: A New Synthesis" (Morgan Kaufmann)
4. S. Russell and P. Norvig, "Artificial Intelligence: A Modern Approach" (Prentice Hall)
5. Christopher Bishop, "Pattern Recognition and Machine Learning" (Springer)
6. Ian Goodfellow, et al., "Deep Learning" (MIT Press)

---

**END OF UNIT III COMPREHENSIVE STUDY MATERIAL**
