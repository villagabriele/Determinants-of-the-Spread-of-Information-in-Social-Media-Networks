## Project Overview

This project investigates how **network topology**, **seeding strategies**, and **diffusion mechanisms** influence the spread of information in social media.

Using a real-world **Facebook politician network** from the SNAP dataset, we simulate and compare three distinct diffusion models (ICM, LTM, SIR) against random graph benchmarks. The study analyzes whether the structural properties of real social networks (clustering, communities) accelerate or hinder information propagation compared to random models.

This work was conducted as part of the **Complex and Social Networks** course at **UPC (Universitat Politècnica de Catalunya)** by me and **Ilaria Boschetto**

## Research Questions & Hypotheses

The project tests three core hypotheses:
1.  **Topology:** Does the structure of real social networks significantly affect diffusion speed compared to random benchmarks (Erdős-Rényi and Degree-Preserving Switching)?
2.  **Seeding:** Do centrality-based seeding strategies (Degree, Betweenness) outperform random seeding in terms of speed and reach?
3.  **Models:** Do different diffusion models (ICM, LTM, SIR) produce significantly different outcomes reflecting their underlying mechanisms?

## Methodology

### 1. Data Source
We utilized the **Facebook Page-Page network** (specifically the `politician` category) from the [Stanford Network Analysis Project (SNAP)](https://snap.stanford.edu/data/gemsec-Facebook.html).
* **Nodes:** 5,908 (Facebook pages)
* **Edges:** 41,729 (Mutual likes/follows)

### 2. Network Benchmarks
To isolate the effects of topology, we compared the real network against:
* **Erdős-Rényi (ER):** Preserves size and density, randomizes connections.
* **Degree-Preserving Switching:** Preserves degree distribution, randomizes clustering and community structure.

### 3. Diffusion Models
We implemented three standard contagion models from scratch in R:
* **Independent Cascade Model (ICM):** Probabilistic spread ($p=0.1$).
* **Linear Threshold Model (LTM):** Adoption based on peer pressure (thresholds).
* **SIR Model:** Epidemic dynamics with recovery ($\beta=0.05, \gamma=0.3$).

### 4. Seeding Strategies
We initiated cascades using 1% of nodes selected via:
* **Random Selection**
* **Degree Centrality** (Hubs)
* **Betweenness Centrality** (Bridges)
The analysis is performed entirely in **R**. Key implementation details include:

* **Libraries:** `igraph` (network manipulation), `tidyverse` (data cleaning), `ggplot2` (visualization).
* **Parallel Computing:** Utilizes `foreach` and `doParallel` to distribute Monte Carlo simulations across CPU cores for efficiency.
* **Simulations:** 10 independent Monte Carlo replications for every combination of Network $\times$ Model $\times$ Strategy (270 total simulations).
* **Statistical Testing:** ANOVA and Tukey HSD tests to validate hypotheses.
