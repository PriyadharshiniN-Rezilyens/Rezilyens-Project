# Rezilyens-Project - 1

## Cyber Risk Assessment Using Graph-Based Clustering
This project performs risk assessment of organizational assets using graph-based techniques on cybersecurity data provided in Project 1 of the Rezilyens internship assignment. Instead of the Bayesian approach, we apply graph modeling, Louvain community detection, and centrality-based scoring to evaluate and rank assets based on their risk exposure.

### Step 1: Load and Build the Graph

I. Loads 4 CSV datasets:
  1. Asset–Vulnerability mapping
  2. Vulnerability–Attack Vector mapping
  3. Threat Actor–Asset targeting
  4. Threat Actor–Attack Vector usage
      
II. Constructs a heterogeneous graph using NetworkX:
  1. Nodes: Assets, Vulnerabilities, Attack Vectors, Threat Actors
  2. Edges: Relationships like has_vulnerability, exploited_by, targets, and uses, with edge attributes like CVSS, exploit probability, and targeting probability.

### Step 2: Visualize the Graph (Graph Construction)
   1. Nodes are colored by type
   2. Edges are labeled by relation

### Step 3: Apply Louvain Clustering
  1. Converts the graph to an undirected version
  2. Applies the Louvain algorithm to detect communities (clusters) of closely connected entities
  3. Assigns Cluster IDs to nodes for group-based analysis

### Step 4: Calculate Risk Scores

i)For each Asset, computes:
  1. Degree and Betweenness Centrality
  2. Average CVSS of connected vulnerabilities
  3. Exploit Probability
  4. Threat Actor Targeting Probability

ii)Uses a weighted formula to calculate a final risk score

iii)Ranks assets from most to least risky

### Step 5: Visualize Risk Rankings
  1. A bar chart of all asset risk scores is generated
  2. Top 5 risky assets are highlighted in red
  3. Makes prioritization of high-risk assets easy

### How to Run
   1. Clone the repo and place the 4 CSV files into the "/dataset" folder.
   2. Run "Project-1.ipynb" or your notebook.
   3. View graphs and generated risk ranking file "asset_risk_analysis.csv".

### Top Risky Assets (Sample Output)

| Asset | Cluster ID | Risk Score |
|-------|------------|------------|
| WebApp-01	| 3 | 2.1063 |
|Workstation-04	| 0 | 2.0708 |
| WebApp-05	| 3	| 2.0597 |
| Server-02 |	1 |	2.0415 |
| Server-01 | 5	| 2.0398 |


