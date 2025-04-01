# Rezilyens-Project - 1
# Graph-Based Risk Assessment in Cybersecurity Using Community Detection Techniques

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

![image](https://github.com/user-attachments/assets/5f8ef3f9-5dfb-4708-9aa7-36be87cb988f)

### Step 2: Visualize the Graph (Graph Construction)
   1. Nodes are colored by type
   2. Edges are labeled by relation

### Step 3: Apply Louvain Clustering
  1. Converts the graph to an undirected version
  2. Applies the Louvain algorithm to detect communities (clusters) of closely connected entities
  3. Assigns Cluster IDs to nodes for group-based analysis

![image](https://github.com/user-attachments/assets/bdddafcc-582f-4c56-80db-0c9814b2649a)

For this project, I chose the Louvain clustering algorithm because it’s efficient, doesn’t require me to predefine the number of clusters, and works well with large, complex graphs like the one I built from the cybersecurity dataset. I explored other options like Spectral Clustering and Label Propagation but found that Spectral requires the number of clusters to be set in advance, and Label Propagation tends to give inconsistent results. Louvain, on the other hand, automatically detects meaningful communities by optimizing modularity, which makes it perfect for identifying related groups of assets, vulnerabilities, and threats. It also gave me clear, interpretable clusters that helped in understanding and prioritizing cyber risks within the network—exactly what I needed for this kind of analysis.

### Step 4: Calculate Risk Scores

i)For each Asset, computes:
  1. Degree and Betweenness Centrality
  2. Average CVSS of connected vulnerabilities
  3. Exploit Probability
  4. Threat Actor Targeting Probability

ii)Uses a weighted formula to calculate a final risk score

iii)Ranks assets from most to least risky

![image](https://github.com/user-attachments/assets/e65fae74-2e9f-4b7b-a7ae-3085167c32ab)

To prioritize which assets are most at risk, I calculated a composite risk score for each one by combining both network-based and vulnerability-based insights. First, I computed degree centrality and betweenness centrality to understand how connected and strategically important an asset is within the graph, because more connected or central assets are generally more exposed. Then, I averaged the CVSS scores and exploit probabilities of vulnerabilities linked to each asset to capture how severe and exploitable those issues are. I also included the probability of being targeted by threat actors, which reflects the likelihood of a real-world attack. All of these metrics were brought together using a weighted formula to generate a final risk score. Assets were then ranked from highest to lowest risk, allowing me to clearly identify which systems (like WebApp-01 and Workstation-04) require the most immediate attention. This approach helped turn complex and interconnected cybersecurity data into clear, actionable insights.

### Step 5: Visualize Risk Rankings
  1. A bar chart of all asset risk scores is generated
  2. Top 5 risky assets are highlighted in red
  3. Makes prioritization of high-risk assets easy

![image](https://github.com/user-attachments/assets/c52810b4-dade-4d0a-8b8d-1c13dd9185d9)

### Top Risky Assets (Sample Output)

| Asset | Cluster ID | Risk Score |
|-------|------------|------------|
| WebApp-01	| 3 | 2.1063 |
|Workstation-04	| 0 | 2.0708 |
| WebApp-05	| 3	| 2.0597 |
| Server-02 |	1 |	2.0415 |
| Server-01 | 5	| 2.0398 |


# Project - 2
# ETL Pipeline for Cyber Threat Intelligence

The Cyber Threat Data Fetcher is a Python-based tool that fetches and processes threat intelligence data for a given IP address from two renowned sources: AbuseIPDB and VirusTotal. This tool allows users to retrieve and analyze data about an IP's reputation, abuse history, and other security-related metrics. The collected data can be further processed, logged, or stored for analysis.


## How It Works
Step-1: Fetch Data from APIs
The script defines two primary functions:
      
   - fetch_abuseipdb_data(ip): Fetches abuse-related data from AbuseIPDB for the given IP address. The function uses the API key to authenticate and sends a request to the AbuseIPDB API. It returns the abuse report data, including the number of reports and abuse confidence score.
      
   - fetch_virustotal_data(ip): Fetches security and reputation-related data from VirusTotal for the given IP address. The function sends a request to the VirusTotal API with the IP address and API key, returning data such as reputation, analysis results, and other metadata.
      
Both functions use requests.get() to send HTTP GET requests to the respective APIs.

Step-2: Data Logging and Error Handling
   - Logging: The script uses Python's logging library to log the execution process, such as when data is being fetched or if an error occurs. This is helpful for debugging and monitoring the program’s behavior.
      
      - logging.info(): Logs general information (e.g., fetching data for a specific IP).
      
      - logging.warning(): Logs warnings, such as when an API request fails.
      
      - logging.error(): Logs errors that occur during the fetching process.
      
   - Error Handling: The script is designed to handle errors gracefully. If an error occurs (e.g., invalid API key, network issue), it logs the error and continues without crashing.
   
![image](https://github.com/user-attachments/assets/cc2c1962-7800-4b39-b288-6ae6a9e822f4)

Step-3: Data Output
After successfully fetching the data, the script logs the returned data from both APIs and provides the following information:
      
  - AbuseIPDB Data: Includes abuse reports, confidence scores, and related metadata.
      
  - VirusTotal Data: Includes reputation, analysis stats, and other related security data.
      
If both APIs return valid data, they will be logged to the console, allowing you to review the information for the given IP address.

![image](https://github.com/user-attachments/assets/faa33cdb-a750-4635-9eb6-ec0716e72555)

Step-4: save this output in cvs file
- successfully saved "threat_data_export.csv"
