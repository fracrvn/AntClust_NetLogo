# AntClust: Bio-inspired Swarm Intelligence Clustering

AntClust is an unsupervised clustering algorithm based on the chemical recognition system used by ants to distinguish nestmates from intruders. This project implements the model in **NetLogo**, providing a decentralized approach where global clustering emerges from local stochastic interactions without needing a predefined number of clusters.

## Biological Foundation
In nature, ants solve a daily recognition problem to protect the nest by forming groups that share a dynamic chemical identity. This identity is constantly updated through social contact, with no central control; each ant maintains its own individual "vision" of the colony odor.

## ⚙Algorithm Architecture
The implementation follows the original theoretical framework by Labroche et al., divided into five distinct phases:

1.  **Initialization**: Data objects are associated with artificial ants, with vectors representing genetic information.
2.  **Ontogenesis (Learning)**: Agents learn an initial **Acceptance Threshold** during a set number of random meetings, scaled as a percentage of the population.
3.  **Interactions**: Agents interact through six social rules (R1–R6):
    * **Constructive Rules**: Creation, Assimilation, and Reinforcement.
    * **Corrective Rules**: Conflict and Competition.
4.  **Nest Cleanup**: Filtering out statistical noise and unstable clusters based on a minimum population threshold.
5.  **Finalization**: Orphans are assigned to valid nests using a 1NN (First Nearest Neighbor) approach.

## 🚀 Technical Enhancements
To optimize stability and explore the algorithm's limits, several advanced features were introduced:

**Sequential Optimization**: The interaction model uses a sequential approach ($75 \times N$ iterations), significantly improving computational efficiency compared to parallel activation.
**Memory Decay ($\lambda$)**: A custom parameter that reduces maximum similarity over time, preventing thresholds from "freezing" on early outliers.
**Learning Rate ($\alpha$)**: A slider-controlled variable to tune the update speed of social estimators ($M$ and $M+$).
**Python Integration**: Uses the `py` extension to connect NetLogo with **scikit-learn**, enabling the calculation of advanced metrics such as Adjusted Rand Index (ARI), Silhouette, Homogeneity, and Completeness.

## Experimental Results
The model was validated through an extensive campaign of over **30,000 simulations** using NetLogo’s BehaviorSpace, with data aggregated over 20 independent runs for each configuration.

| Dataset | Objects | Attributes | Classes | Max ARI Achieved |
| :--- | :--- | :--- | :--- | :--- |
| **Iris** | 150 | 4 | 3 | **0.618**  |
| **Breast Cancer** | 569 | 30 | 2 | **0.725**  |
| **Glass** | 214 | 9 | 6 | **0.198** (High imbalance)  |

*The results show that the model excels in capturing data structure and efficiently scaling in high-dimensional spaces like the Breast Cancer dataset.*

## Repository Structure
* `/model`: NetLogo `.nlogo` source code.
* `/dataset`: Datasets (Iris, Glass, Breast Cancer) and result tables.
* `/analysis`: Scripts for statistical processing and parameter calibration.
* `/docs`: Final presentation and detailed documentation.

## Requirements
* **NetLogo 7.x**
* **Python 3.x** (with `scikit-learn` installed)
* **NetLogo `py` extension**