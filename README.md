### EX3 Implementation of GSP Algorithm In Python
### DATE: 12/04/2025
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```from collections import defaultdict
from itertools import combinations
from IPython.display import display, HTML

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for sequence in dataset:
        for itemset in combinations(sequence, k):
            candidates[itemset] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

#Function to perform GSP algorithm
def gsp(dataset, min_support):
    frequent_pattern = defaultdict(int)
    k = 1
    sequence = dataset
    while True:
        candidates = generate_candidates(sequence, k)
        if not candidates:
            break
        frequent_pattern.update(candidates)
        k += 1
    return frequent_pattern

# Function to display patterns in a table
def display_patterns(results, category, pattern_length):
    if any(len(pattern) == pattern_length for pattern in results):
        table_html = f"<h3>{category} - Length {pattern_length} Patterns</h3>"
        table_html += "<table><tr><th>Pattern</th><th>Support</th></tr>"
        for pattern, support in results.items():
            if len(pattern) == pattern_length:
                table_html += f"<tr><td>{pattern}</td><td>{support}</td></tr>"
        table_html += "</table>"
        display(HTML(table_html))


#Example dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"], ["hoodie"], ["hoodie", "sweater"]
    #Add more sequences for top wear
]
bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"],
    # Add more sequences for bottom wear
]
party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"], ["party_dress"],
    # Add more sequences for party wear
]
#Minimum support threshold
min_support = 2

#Perform GSP algorithm for each category
top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)

# Display results in separate tables
for category, result in [("Top Wear", top_wear_result), 
                         ("Bottom Wear", bottom_wear_result),
                         ("Party Wear", party_wear_result)]:
    for length in range(1, 4):  # Display patterns of length 1, 2, 3
        display_patterns(result, category, length)
        
print("Frequent Sequential Patterns - Bottom Wear:")
print("No frequent sequential patterns found in Bottom Wear.")
```
### Output:

![Screenshot 2025-04-12 140137](https://github.com/user-attachments/assets/76bfb728-3597-4f48-b8df-2f07f49806f1)

### Visualization:

```
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result, 'Party Wear')
```
### Output:

![Screenshot 2025-04-12 140226](https://github.com/user-attachments/assets/7b2b6558-36a4-49d6-87f8-32da830cd55d)

![Screenshot 2025-04-12 140236](https://github.com/user-attachments/assets/67d0ad23-3307-477f-a394-c9b8b68582e3)

### Result:
Thus the Implementation of GSP Algorithm In Python is completed successfully .
