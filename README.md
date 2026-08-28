# PseudoFold

**Efficient Prediction of RNA Secondary Structures with Pseudoknots Using Sparse Dynamic Programming**

PseudoFold is a Python-based tool for predicting and visualizing **RNA secondary structures**, including pseudoknots. The project combines a sparse dynamic programming approach for base-pair prediction with a greedy post-processing method for pseudoknot detection.

## Overview

RNA secondary structure plays an important role in understanding RNA function. Traditional Nussinov-style approaches can predict base pairing but generally do not directly handle pseudoknots.

PseudoFold addresses this by combining:

1. **Sparse dynamic programming** for predicting RNA base pairs
2. **Greedy post-processing** for detecting pseudoknots
3. **Approximate energy scoring** for evaluating predicted structures
4. **Arc-diagram visualization** for representing the resulting RNA structure

The tool accepts an RNA sequence and produces its predicted structure, base pairs, pseudoknot pairs, and approximate free-energy values.

## Key Features

* RNA secondary-structure prediction
* Sparse dynamic programming matrix
* Canonical base-pair detection
* Minimum loop-length constraint
* Pseudoknot detection using greedy post-processing
* Dot-bracket representation
* Approximate free-energy calculation
* RNA arc-diagram visualization
* Support for `A`, `U`, `G`, and `C`
* `T` accepted as an alias for `U`
* Input validation

## Methodology

### 1. Sequence Input

The program accepts an RNA sequence containing:

```text
A, U, G, C
```

DNA-style `T` is also accepted and converted to `U`.

### 2. Base Pairing

The implementation uses the following pairing energies:

| Base Pair | Energy |
| --------- | -----: |
| A-U       |   -2.0 |
| U-A       |   -2.0 |
| C-G       |   -3.0 |
| G-C       |   -3.0 |
| G-U       |   -1.0 |
| U-G       |   -1.0 |

A minimum loop length of **3** is used.

### 3. Sparse Dynamic Programming

Instead of storing the complete dynamic programming matrix, PseudoFold uses a sparse matrix representation.

The dynamic programming procedure evaluates possible structures through:

* skipping the left base
* skipping the right base
* pairing compatible bases
* splitting the sequence into subproblems

The structure is reconstructed using traceback information.

### 4. Pseudoknot Detection

After the main dynamic programming prediction, a greedy post-processing step searches for compatible unpaired bases that can form additional pairs.

These pairs are identified separately as pseudoknot pairs.

### 5. Dot-Bracket Representation

Standard base pairs are represented using:

```text
( )
```

Pseudoknot pairs are represented using:

```text
[ ]
```

This provides a compact representation of the predicted structure.

### 6. Arc Diagram

The project also generates an RNA arc diagram using Matplotlib.

The visualization distinguishes:

* Base-paired positions
* Unpaired positions
* Pseudoknot positions
* RNA backbone
* Standard base-pair arcs
* Pseudoknot arcs

## Input

The program accepts a raw RNA sequence through console input.

Example:

```text
Enter your RNA sequence (A,U,G,C or A,T,G,C):
AUGCUAGCUAGCUA
```

The program validates the sequence before performing the prediction.

## Output

PseudoFold reports:

```text
Sequence
Dot-bracket structure
Base pairs
Pseudoknot pairs
Approximate free energy without pseudoknots
Pseudoknot energy contribution
Approximate total free energy including pseudoknots
```

It also displays an RNA arc diagram.

## Simulation Parameters

| Parameter               | Value                  |
| ----------------------- | ---------------------- |
| Typical sequence length | 10–200 nt              |
| Accepted bases          | A, U, G, C             |
| T handling              | T → U                  |
| Minimum loop length     | 3                      |
| Dynamic programming     | Sparse, bottom-up      |
| Pseudoknot detection    | Greedy post-processing |
| Visualization           | Matplotlib arc diagram |
| Recursion limit         | 3000                   |

## Technologies

* **Python**
* **NumPy**
* **Matplotlib**
* Python `collections`
* Python `sys`



## Concepts Demonstrated

* RNA secondary structure
* Dynamic programming
* Sparse matrix representation
* Traceback
* Greedy algorithms
* Pseudoknot detection
* Dot-bracket notation
* Free-energy scoring
* Computational biology
* Data visualization

## Limitations

The energy model used by the project is an **approximate scoring model** based on predefined base-pair energies. Pseudoknot detection is performed using greedy post-processing rather than an exhaustive optimization procedure.

Therefore, the predictions are intended as a computational and educational approach to RNA structure prediction rather than a replacement for experimentally validated structures or comprehensive thermodynamic prediction systems.

## Future Improvements

Potential extensions include:

* More comprehensive thermodynamic energy models
* Improved pseudoknot optimization
* Additional RNA structural motifs
* Larger benchmark datasets
* Comparison with established RNA structure prediction tools
* Interactive visualization
* Graphical user interface
* Performance optimization for longer sequences


The project was developed as an academic implementation exploring dynamic programming, greedy algorithms, and their application to computational RNA structure prediction.
