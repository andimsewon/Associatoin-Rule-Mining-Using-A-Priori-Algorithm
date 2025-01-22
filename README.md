# Readme

## Decision Tree Implementation in Python

This repository contains a Python implementation of a Decision Tree algorithm using the Information Gain method. The code is designed to read data from a CSV file, build a decision tree, and display the tree in an `if-then` format for better interpretability.

---

## Features

1. **Custom Data Structure**: The `Data` class is used to store feature-value pairs and corresponding labels.
2. **Entropy and Information Gain**: Core functions for calculating entropy and information gain are implemented to select the best feature for splitting at each node.
3. **Tree Representation**: The decision tree is represented using the `Node` class, which contains feature information, label information, and child nodes.
4. **Readable Output**: The decision tree is displayed in a user-friendly `if-then` format for better understanding.

---

## Association Rule Mining and the Importance of the A-Priori Algorithm

### Association Rule Mining

Association Rule Mining is a technique used to discover relationships or patterns among items within a dataset. It is widely applied in fields like market basket analysis, recommendation systems, and customer behavior analysis. The key metrics used in Association Rule Mining include:

- **Support**: Indicates how frequently a specific itemset appears in the dataset.  
- **Confidence**: Represents the likelihood that a certain itemset leads to another.  
- **Interest**: Measures the difference between confidence and the expected frequency of the itemset, reflecting both positive and negative associations.

### Importance of the A-Priori Algorithm

The **A-Priori Algorithm** is a foundational method in Association Rule Mining. It efficiently identifies frequent itemsets by iteratively generating and evaluating candidate itemsets based on the principle of monotonicity (if an itemset is infrequent, all its supersets are also infrequent). The algorithm operates in two main passes:

1. **Pass 1**: Scans the database to calculate the frequency of single items and filters items below the minimum support threshold.  
2. **Pass 2**: Uses the frequent items from Pass 1 to generate larger itemsets (e.g., pairs, triplets) and evaluates their frequencies.

The A-Priori Algorithm is crucial for mining association rules in large datasets, as it systematically reduces the search space, focusing only on candidate itemsets with sufficient support. This makes it a cornerstone of association rule mining methodologies.

---

## Requirements

- Python 3.x
- No external libraries are required. Only built-in libraries such as `csv`, `math`, `sys`, and `collections` are used.

---

## Usage

### Input Data Format

The input CSV file should follow these conventions:
- The first row contains the headers.
- Each subsequent row represents a data sample.
- The last column contains the labels.

Example (`playtennis.csv`):

| Outlook | Temperature | Humidity | Wind | PlayTennis |
|---------|-------------|----------|------|------------|
| Sunny   | Hot         | High     | Weak | No         |
| Overcast| Hot         | High     | Strong| Yes       |

## Output
The Decision tree is printed in an if-then format. For example:

IF Outlook == Sunny AND Humidity == High THEN No
IF Outlook == Sunny AND Humidity == Normal THEN Yes
IF Outlook == Overcast THEN Yes
IF Outlook == Rain AND Wind == Weak THEN Yes
IF Outlook == Rain AND Wind == Strong THEN No

### Running the Code

Run the script from the command line, passing the path to the CSV file as an argument:

```bash
python aPriori.py playtennis.csv



