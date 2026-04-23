# Medan Flood Evacuation Route Optimization using A* Algorithm

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![OSMnx](https://img.shields.io/badge/OSMnx-2.1.0-orange) ![NetworkX](https://img.shields.io/badge/NetworkX-3.1-green) ![Folium](https://img.shields.io/badge/Folium-latest-blueviolet)

## Project Overview
This project implements a **Graph-based Navigation System** to find optimal evacuation routes during major flood events in **Medan, Indonesia**. By leveraging historical flood data (2020–2025) and real-world road networks from **OpenStreetMap**, the system calculates safe paths that bypass submerged areas using the **A* (A-Star) Algorithm**.

## Key Features
- **Real Road Network**: Fetches and processes over 42,000 nodes and 99,000 edges of Medan's road network using `OSMnx`.
- **Dynamic Flood Simulation**: Simulates three severity scenarios (Light, Medium, Severe) based on historical news data.
- **Adaptive Pathfinding**: Uses A* with a **Haversine Heuristic** to find the shortest physical distance while avoiding blocked roads.
- **Zone-Exit Logic**: Includes a BFS (Breadth-First Search) mechanism for victims trapped inside flood zones to find the nearest safe access point before navigating to a shelter.
- **Interactive Visualization**: Generates a web-based map (`Folium`) displaying flood zones, shelters, and computed routes.

## Technical Methodology

### 1. Data Modeling
- **Graph Construction**: The road network is modeled as a directed graph where nodes are intersections and edges are road segments.
- **Cost Function**: $f(n) = g(n) + h(n)$
  - $g(n)$: Actual distance from the origin.
  - $h(n)$: Estimated distance to the goal (Haversine formula).

### 2. Flood Constraints
Roads are marked as **blocked** only if both connecting nodes are within a 300m radius of a flood epicenter. This ensures that 'escape routes' leading out of a zone remain visible to the algorithm.

### 3. Simulation Scenarios
- **Scenario A**: 3 active flood points (Light).
- **Scenario B**: 5 active flood points (Moderate).
- **Scenario C**: 8 active flood points (Severe - based on Nov 2025 events).

## Results Summary
| Scenario | Success Rate | Avg. Distance | Key Observation |
|---|---|---|---|
| Light | 87.5% | 4.79 km | Most routes are direct. |
| Moderate | 87.5% | 4.80 km | Some detours required in Central Medan. |
| Severe | 87.5% | 5.04 km | Significant rerouting; certain areas isolated. |

> **Note**: The *Brigjend Katamso* area consistently showed as 'Isolated', highlighting a critical need for additional emergency shelters or boat-based evacuation in that specific district.

## How to Use
1. **Environment Setup**:
   ```bash
   pip install osmnx folium networkx
   ```
2. **Run the Notebook**: Execute cells sequentially to download the Medan graph, define epicenters, and run the pathfinding logic.
3. **View the Map**: Open the generated `peta_evakuasi_medan.html` in any web browser to interact with the visual results.

## References
- Boeing, G. (2017). *OSMnx: New methods for acquiring, constructing, analyzing urban street networks*.
- Hart, P. E., et al. (1968). *A Formal Basis for the Heuristic Determination of Minimum Cost Paths*.
- Data Source: **OpenStreetMap** contributors & **BNPB Indonesia** (National Disaster Management Authority).
