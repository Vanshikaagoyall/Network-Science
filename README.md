# Neighborhood Coreness Centrality (NCC)

A Python implementation and experimental analysis of **Neighborhood Coreness Centrality (NCC)** for identifying and ranking influential nodes in complex networks.

This project implements NCC using **k-core/coreness information** and the coreness values of a node's neighbours. It also applies the measure to the **Karate Club Network** and **Dolphin Social Network**, generates visualizations, ranks the top 10 nodes, and compares the results across the two networks.

---

## 📌 About the Project

In a complex network, some nodes are more influential than others. Traditional centrality measures such as Degree Centrality, Betweenness Centrality, Closeness Centrality, PageRank, and K-shell centrality are commonly used to identify important nodes.

However, K-shell centrality can assign the same score to multiple nodes belonging to the same shell. **Neighborhood Coreness Centrality** addresses this limitation by considering not only the coreness of a node but also the coreness of its neighbours.

The core idea is:

> A node connected to highly coreness-ranked neighbours can be considered more structurally important within the network.

The project follows the NCC approach discussed in the work by Bae and Kim (2014), with further context from the neighborhood-coreness voting approach of Kumar and Panda (2020).

---

## 🧠 NCC Formula

For a node `v`, the Neighborhood Coreness Centrality is calculated as:

$$
NCC(v) = \sum_{u \in N(v)} Core(u)
$$

where:

- `N(v)` = set of neighbours of node `v`
- `Core(u)` = k-shell/coreness value of neighbour `u`

The implementation then normalizes the NCC value:

$$
NCC_{norm}(v) = \frac{NCC(v)}{\max_{x \in V} NCC(x)}
$$

The final value is rounded to four decimal places.

---

## 🔍 How the Implementation Works

The main function is:

```python
neighborhood_coreness_centrality(G, node)
```

The function performs the following steps:

1. Calculates the coreness of every node using `NetworkX`.
2. Finds all neighbours of the selected node.
3. Adds the coreness values of those neighbours.
4. Calculates NCC values for all nodes.
5. Finds the maximum NCC value.
6. Normalizes the selected node's NCC.
7. Returns the normalized value rounded to four decimal places.

The implementation uses:

```python
coreness = nx.core_number(G)
```

and calculates the neighbourhood contribution using the coreness of adjacent nodes.

---

## Networks Used

### 1. Karate Club Network

The project uses the built-in NetworkX Karate Club graph:

```python
G = nx.karate_club_graph()
```

The network contains 34 nodes representing relationships in the Zachary Karate Club network.

The implementation:

- Visualizes the network.
- Calculates NCC for every node.
- Sorts nodes by NCC.
- Extracts the top 10 nodes.
- Generates a bar chart of their normalized NCC scores.

### Top 10 Karate Network Nodes

| Rank | Node | NCC |
|---:|---:|---:|
| 1 | 0 | 1.0000 |
| 2 | 33 | 0.9796 |
| 3 | 2 | 0.7347 |
| 4 | 32 | 0.7143 |
| 5 | 1 | 0.6327 |
| 6 | 3 | 0.4490 |
| 7 | 31 | 0.4286 |
| 8 | 8 | 0.4082 |
| 9 | 13 | 0.4082 |
| 10 | 23 | 0.3469 |

These values are produced directly by the code in this repository.

---

### 2. Dolphin Social Network

The project also evaluates the Dolphin Social Network using:

```python
G = nx.read_gml("dolphins.gml")
```

The network is visualized and NCC is calculated for every dolphin.

The implementation then ranks the nodes and extracts the top 10.

### Top 10 Dolphin Network Nodes

| Rank | Node | NCC |
|---:|---|---:|
| 1 | Grin | 1.0000 |
| 2 | Topless | 0.9348 |
| 3 | SN4 | 0.8913 |
| 4 | Scabs | 0.7826 |
| 5 | Kringel | 0.7609 |
| 6 | Patchback | 0.7174 |
| 7 | SN9 | 0.6957 |
| 8 | Trigger | 0.6739 |
| 9 | Beescratch | 0.6522 |
| 10 | Web | 0.6522 |

---

## Visualizations

The project generates:

- Network visualization of the Karate Club Network
- NCC values for individual nodes
- Top 10 NCC nodes for the Karate network
- Network visualization of the Dolphin Social Network
- NCC values for individual dolphins
- Top 10 NCC nodes for the Dolphin network
- Comparative analysis of the top-ranked nodes

The original notebook output also contains bar charts showing the normalized NCC scores of the top 10 nodes.

---

## Tech Stack

- **Python**
- **NetworkX** – graph and network analysis
- **Matplotlib** – network and result visualization
- **Google Colab / Jupyter Notebook** – execution environment

---

## Installation

Install the required Python libraries:

```bash
pip install networkx matplotlib
```

If you are using Google Colab:

```python
!pip install networkx matplotlib
```

---

## How to Run

### Step 1: Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### Step 2: Install dependencies

```bash
pip install networkx matplotlib
```

### Step 3: Add the Dolphin dataset

Make sure the file:

```text
dolphins.gml
```

is present in the working directory.

### Step 4: Run the notebook/script

Run the NCC implementation and execute the Karate and Dolphin network sections.

The program will calculate normalized NCC values, print node rankings, and generate visualizations.

---

## Project Structure

```text
Neighborhood-Coreness-Centrality/
│
├── neighborhood_coreness_centrality.ipynb
├── dolphins.gml
├── README.md
└── ...
```

> If your repository uses a different notebook or Python filename, update the structure above accordingly.

---

## 🧮 Example

For a node `v` whose neighbours have coreness values:

```text
3, 3, 3
```

its NCC is:

\[
NCC(v) = 3 + 3 + 3 = 9
\]

If the maximum NCC in the network is `12`, then:

$$
NCC_{norm}(v) = \frac{9}{12} = 0.75
$$

---

## Applications

Neighborhood Coreness Centrality can be useful for identifying structurally influential nodes in applications such as:

- Social network analysis
- Information diffusion
- Viral marketing
- Rumor control
- Epidemic management
- Community analysis
- Influence maximization
- Network science research

---

## Advantages

- Incorporates the structural position of neighbouring nodes.
- Provides more differentiation than K-shell alone.
- Produces a ranked list of nodes rather than only grouping nodes by shell.
- Uses local neighbourhood information together with global k-core structure.
- Can be efficiently implemented using NetworkX.

---

## Limitations

- NCC depends on the k-core/coreness structure of the network.
- The measure primarily uses the coreness of neighbouring nodes.
- Connections removed during the k-core decomposition are not directly represented in the final neighbourhood score.
- Results can vary depending on the structure and k-core distribution of the network.

---

## References

1. J. Bae and S. Kim, **"Identifying and ranking influential spreaders in complex networks by neighborhood coreness,"** *Physica A*, vol. 395, pp. 549–559, 2014.
2. S. Kumar and B. S. Panda, **"Identifying influential nodes in Social Networks: Neighborhood Coreness based voting approach,"** *Physica A*, vol. 553, 124215, 2020.
3. V. Batagelj and M. Zaversnik, **"An O(m) Algorithm for Cores Decomposition of Networks,"** 2003.
4. R. A. Rossi and N. K. Ahmed, **"The Network Data Repository with Interactive Graph Analytics and Visualization,"** AAAI, 2015.
5. W. W. Zachary, **"An Information Flow Model for Conflict and Fission in Small Groups,"** *Journal of Anthropological Research*, 1977.
6. NetworkX Developers, **"core_number — NetworkX Documentation."**
7. Generative AI tools including ChatGPT, Claude, and Gemini were used as supporting tools during the project/documentation process.

---

## Authors

**Dhruv Nailwal**  
**Vanshika Goyal**

---

## Project Objective

The main objective of this project is to implement and demonstrate **Neighborhood Coreness Centrality** as a network-analysis technique for identifying influential nodes, and to observe how the ranking behaves across different real-world network structures.

If you find this project useful, consider giving the repository a ⭐.
