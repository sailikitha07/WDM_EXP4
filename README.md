### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
import pandas as pd 
import matplotlib.pyplot as plt 
# Read CSV file 
df = pd.read_csv("clustervisitor.csv") 
# Select Age feature 
X = df["Age"].tolist() 
# Number of clusters 
k = 3 
# Step 1: Choose initial centroids (first k values) 
centroids = X[:k] 
  while True: 
    clusters = [[] for _ in range(k)] 
    labels = [] 
    # Step 2: Assign each data point to the nearest centroid 
    for value in X: 
        distances = [abs(value - c) for c in centroids] 
        cluster = distances.index(min(distances)) 
        clusters[cluster].append(value) 
        labels.append(cluster) 
    # Step 3: Calculate new centroids 
    new_centroids = [] 
    for cluster in clusters: 
        if len(cluster) > 0: 
            new_centroids.append(sum(cluster) / len(cluster)) 
        else: 
            new_centroids.append(0) 
    # Step 4: Stop if centroids do not change 
    if new_centroids == centroids: 
        break 
      centroids = new_centroids 
# Add cluster labels to DataFrame 
df["Cluster"] = labels 
# Display complete dataset 
print("Complete Dataset") 
print(df) 
print("\nVisitor Segmentation (Cluster-wise)\n") 
# Display cluster-wise output 
for i in range(k): 
    print(f"Cluster {i}") 
    print(df[df["Cluster"] == i]) 
    print("-" * 50) 
```
### Output:
<img width="588" height="580" alt="image" src="https://github.com/user-attachments/assets/557931f9-ee82-489c-b59b-5c51d10963f4" />
<img width="493" height="251" alt="image" src="https://github.com/user-attachments/assets/f50e5e0e-e112-4b55-9fdd-abcaf0f36024" />

### Visualization:
```python
plt.figure(figsize=(8,6))	 
colors = ["red", "blue", "green"] 
 for i in range(k): 
    cluster_data = df[df["Cluster"] == i] 
    plt.scatter(cluster_data["Age"], 
                cluster_data["Cluster"], 
                color=colors[i], 
                s=80, 
                label=f"Cluster {i}") 

plt.xlabel("Age") 
plt.ylabel("Cluster") 
plt.title("Visitor Segmentation using K-Means") 
plt.legend() 
plt.grid(True) 
plt.show() 
```
### Output:
<img width="671" height="525" alt="image" src="https://github.com/user-attachments/assets/4d842eca-aae1-4d00-90f4-e97b1f00c553" />


### Result:
Thus Cluster and Visitor Segmentation for Navigation patterns in Python is implemented.
