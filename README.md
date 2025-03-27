# Rezilyens-Project

📊 Cyber Risk Assessment Using Graph-Based Clustering
This project performs risk assessment of organizational assets using graph-based techniques on cybersecurity data provided in Project 1 of the Rezilyens internship assignment.

Instead of the Bayesian approach, we apply graph modeling, Louvain community detection, and centrality-based scoring to evaluate and rank assets based on their risk exposure.

📁 Project Structure
**/
├── dataset/
│   ├── asset_vulnerability_mapping.csv
│   ├── attack_vulnerability_mapping.csv
│   ├── prior_attack_success_rate.csv
│   └── threat_actor_asset_targeting.csv
├── risk_analysis.py
├── requirements.txt
├── README.md
└── asset_risk_analysis.csv
**

✅ Project Highlights
Graph Modeling:
Built a heterogeneous graph from 4 CSV datasets (assets, vulnerabilities, attack vectors, and threat actors) using NetworkX.

Community Detection:
Used the Louvain algorithm to identify clusters (communities) of connected entities, revealing sub-networks and attack surfaces.

Risk Scoring:
For each asset, calculated a composite risk score based on:

Degree and betweenness centrality

Average CVSS severity of vulnerabilities

Exploit probabilities

Threat actor targeting likelihood

Community (cluster) risk context

Visualization:

Graph of all entities and their relationships

Louvain clusters

Bar chart showing risk scores, highlighting top risky assets


📊 Top Risky Assets (Sample Output)
Asset	Cluster ID	Risk Score
WebApp-01	3	2.1063
Workstation-04	0	2.0708
WebApp-05	3	2.0597
Server-02	1	2.0415
Server-01	5	2.0398
Assets with the highest risk scores should be prioritized for mitigation and monitoring.

# **How to Run**
1. Clone the repo and add the CSV files into the /dataset folder.

2. Run risk_analysis.py or Jupyter notebook.

3. View visualizations and ranked asset risk report.


