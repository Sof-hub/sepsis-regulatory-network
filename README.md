# Sepsis Regulatory Network Data

Network data files for **Figure 2** of the manuscript:  
**"Regulatory Genetic Variants in Sepsis and Malaria: From Association to Function"**

## Overview

This repository contains the gene regulatory network data illustrating the immune response mechanisms in sepsis. The network integrates:

- **Central hub transcription factors** (NF-κB, IRF1/7, STAT family)
- **Downstream immune response genes** 
- **Regulatory SNPs** that modulate enhancer activity and transcription factor binding
- **Gene-gene and gene-variant interactions**

The network demonstrates how genetic variation influences immune regulatory pathways during severe infection, providing mechanistic insights into sepsis susceptibility.

## Repository Contents
```
sepsis-regulatory-network/
        ├── README.md # This file
        ├── sepsis_network_nodes.csv # Network nodes (genes, TFs, SNPs)
        ├── sepsis_network_edges.csv # Network edges (interactions)
        └── LICENSE # CC0 License
```

## Data Files

### 1. `sepsis_network_nodes.csv`

Contains all network nodes with the following columns:

| Column | Description | Example |
|--------|-------------|---------|
| `id` | Unique node identifier | `STAT1`, `rs143356980` |
| `label` | Node display name | `STAT1`, `CISH_enhancer` |
| `type` | Node category | `transcription_factor`, `gene`, `SNP` |
| `node_color` | Color code for visualization | `blue`, `red`, `green`, `gray` |
| `connectivity` | Number of connections (degree) | `15`, `8`, `3` |

**Node Types:**
- 🔵 **Blue circles**: Hub transcription factors (STAT1, IRF1/7, NF-κB)
- ⬜ **Gray squares**: Target immune genes
- 🔴 **Red diamonds**: Risk-associated regulatory SNPs
- 🟢 **Green diamonds**: Protective regulatory SNPs

### 2. `sepsis_network_edges.csv`

Contains all network interactions with the following columns:

| Column | Description | Example |
|--------|-------------|---------|
| `source` | Origin node ID | `STAT1` |
| `target` | Target node ID | `CISH` |
| `interaction_type` | Type of regulatory interaction | `transcriptional_activation`, `enhancer_binding` |
| `edge_thickness` | Interaction strength | `2.5`, `5.0` |
| `edge_color` | Edge visualization color | `green`, `red` |

**Interaction Types:**
- **transcriptional_activation**: TF activates gene expression
- **transcriptional_repression**: TF represses gene expression  
- **enhancer_binding**: TF binds to enhancer element
- **SNP_modulates**: Genetic variant affects TF binding or enhancer activity

## Network Visualization

The network was created using **Cytoscape v3.10.0** with the following characteristics:

- **Layout**: Force-directed (organic layout)
- **Node size**: Proportional to connectivity (degree)
- **Edge thickness**: Represents interaction strength
- **Color coding**: Indicates functional role (TF, gene, risk/protective variant)

### Key Network Features

- **Scale-free topology**: Few highly connected hubs, many peripheral nodes
- **Modularity**: Clustered around inflammatory signaling pathways
- **Regulatory layers**: TFs → genes → phenotypes

## Biological Context

### Central Hub Transcription Factors

1. **STAT family** (STAT1, STAT3, STAT5)
   - JAK-STAT signaling pathway
   - Cytokine-induced gene expression
   - Interferon response

2. **IRF family** (IRF1, IRF7, IRF9)
   - Interferon regulatory factors
   - Antiviral and antimicrobial responses
   - Type I interferon signaling

3. **NF-κB family** (RELA, NFKB1)
   - Pro-inflammatory gene expression
   - Innate immune activation
   - Cytokine production (TNF-α, IL-6, IL-1β)

### Key Target Genes

- **CISH**: Cytokine-inducible SH2-containing protein (negative regulator)
- **IL6, IL10, IL12**: Pro- and anti-inflammatory cytokines
- **TNF**: Tumor necrosis factor
- **IFNG**: Interferon gamma
- **TLR4**: Toll-like receptor 4

### Regulatory SNPs

Network includes variants:
- Located in enhancer regions
- Affecting transcription factor binding motifs
- Associated with sepsis mortality in GWAS studies
- Validated through functional assays (MPRA, CRISPR screens)

## Usage

### Loading in Cytoscape

1. **Open Cytoscape** (download from https://cytoscape.org)
2. **Import Network**: File → Import → Network from File
3. Select `sepsis_network_edges.csv`
4. **Import Node Attributes**: File → Import → Table from File
5. Select `sepsis_network_nodes.csv`
6. **Apply Style**: Use columns `node_color`, `edge_color`, `edge_thickness`

### Loading in R

```r
# Load required libraries
library(igraph)
library(tidyverse)

# Read data
nodes <- read_csv("sepsis_network_nodes.csv")
edges <- read_csv("sepsis_network_edges.csv")

# Create igraph object
network <- graph_from_data_frame(d = edges, vertices = nodes, directed = TRUE)

# Basic network statistics
vcount(network)  # Number of nodes
ecount(network)  # Number of edges
degree(network)  # Connectivity distribution
```

### Loading in Python

```
import pandas as pd
import networkx as nx

# Load data
nodes = pd.read_csv('sepsis_network_nodes.csv')
edges = pd.read_csv('sepsis_network_edges.csv')

# Create NetworkX graph
G = nx.from_pandas_edgelist(edges, 
                             source='source', 
                             target='target', 
                             edge_attr=True,
                             create_using=nx.DiGraph())

# Add node attributes
node_attrs = nodes.set_index('id').to_dict('index')
nx.set_node_attributes(G, node_attrs)

# Basic statistics
print(f"Nodes: {G.number_of_nodes()}")
print(f"Edges: {G.number_of_edges()}")
```

## Citation

@misc{sepsis-network-2026,
  author = {Quinteros, S.},
  title = {Sepsis Regulatory Network Data},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/Sof-hub/sepsis-regulatory-network}
}

## Associated manuscript:

Quinteros, S. (2026). Regulatory Genetic Variants in Sepsis and Malaria: From Association to Function. Aix Marseille University.

## Related Resources
Cytoscape: https://cytoscape.org

GTEx Portal: https://gtexportal.org (eQTL data)

GWAS Catalog: https://www.ebi.ac.uk/gwas (variant associations)

ENCODE: https://www.encodeproject.org (regulatory elements)

## Contact
For questions or feedback:

GitHub Issues: Create an issue

Email: sofia.quinteros@etu.univ-amu.fr

Last updated: January 2026
Version: 1.0



