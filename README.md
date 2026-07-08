# Graph-Based Transportation Network Analysis Using Python

## Project Overview

This project models a real-world transportation network as a graph and analyzes how network disruptions affect accessibility. The implementation uses the 2018 Kerala floods as a case study to evaluate how road closures and degraded road conditions influence access to essential services.

The primary objective of the project is not flood modelling itself, but the development of a computational workflow that combines graph modelling, shortest path algorithms, geospatial data processing, and network analysis to support infrastructure restoration decisions.

The entire workflow is implemented in Python using publicly available OpenStreetMap data.

---

## Problem Statement

Transportation networks often experience partial failures during natural disasters. When roads become inaccessible, the shortest routes to critical facilities such as hospitals may change significantly.

Given a road network:

- model different road conditions after a disruption,
- measure the resulting accessibility changes,
- identify the most affected regions,
- simulate restoration of damaged infrastructure, and
- rank restoration priorities based on their impact on overall network accessibility.

The 2018 Kerala floods provide the real-world context used to demonstrate this workflow.

---

## Methodology

### 1. Road Network Construction

The transportation network is downloaded from OpenStreetMap using OSMnx and represented as a graph.

- Nodes represent road intersections.
- Edges represent road segments.
- Bridges, rivers and public infrastructure are extracted from OpenStreetMap tags.

The extracted infrastructure includes:

- Hospitals
- Schools
- Police stations
- Fire stations
- Bus stations
- Bridges
- Major rivers

---

### 2. Data Validation

Before performing any analysis, the extracted data is validated.

Validation includes:

- graph connectivity
- duplicate infrastructure detection
- infrastructure counts
- bridge extraction
- river extraction

This ensures that the graph is suitable for shortest path analysis.

---

### 3. Flood Scenario Simulation

A simplified flood scenario is generated using the proximity of roads to major rivers.

Each road segment is classified into one of three categories:

- Open
- Waterlogged
- Closed

Each category is assigned a different traversal cost.

Instead of modifying shortest path algorithms, the graph itself is updated by assigning different edge weights to represent changing road conditions.

---

### 4. Accessibility Analysis

Hospitals are treated as multiple destination nodes.

Accessibility is evaluated using **NetworkX Multi-Source Dijkstra's Algorithm**, which computes the shortest travel cost from every node in the road network to the nearest hospital.

The analysis is performed twice:

- Before flooding
- After flooding

The implementation computes:

- shortest travel cost before flooding
- shortest travel cost after flooding
- increase in travel cost
- percentage increase
- accessibility statistics
- distribution of accessibility loss

---

### 5. Bridge Restoration Simulation

Each closed bridge is restored individually while keeping all other flood conditions unchanged.

For every restoration:

1. the bridge travel cost is restored,
2. Multi-Source Dijkstra is executed again,
3. average accessibility is recomputed,
4. the improvement is recorded.

The bridges are then ranked according to the reduction in average network-wide travel cost after restoration.

This produces a restoration priority list based entirely on graph analysis.

---

## Technologies Used

- Python
- NetworkX
- OSMnx
- GeoPandas
- Pandas
- NumPy
- Matplotlib
- Shapely

---

## Algorithms Used

The project uses the following algorithms and computational techniques:

- Graph modelling of road networks
- Multi-Source Dijkstra shortest path algorithm
- Geospatial buffering
- Spatial nearest-neighbour mapping
- Network accessibility analysis
- Simulation-based infrastructure restoration ranking

---

---

## Usage

Open the notebook and execute the cells sequentially.

The notebook performs the following steps automatically:

1. Downloads the road network from OpenStreetMap.
2. Extracts infrastructure and river data.
3. Builds the transportation graph.
4. Simulates flood-induced road conditions.
5. Computes accessibility before and after flooding.
6. Evaluates the effect of restoring each closed bridge.
7. Produces a ranked list of restoration priorities.

---

## Results

The implementation produces:

- transportation network graph
- infrastructure validation summaries
- flood scenario visualization
- accessibility statistics before and after disruption
- accessibility loss distribution
- ranked bridge restoration priorities

The final output is a decision-support ranking showing which bridge restoration yields the greatest improvement in network accessibility.

---

## Limitations

The project intentionally uses a simplified disruption model.

- Flood extent is approximated using river proximity rather than observed inundation maps.
- Travel cost is represented using weighted edge penalties.
- Accessibility is evaluated only with respect to hospitals.
- Temporal traffic conditions are not included.

These assumptions keep the focus on graph algorithms and network analysis rather than hydrological modelling.

---

## Future Improvements

Possible extensions include:

- using observed flood inundation maps
- incorporating real traffic speeds
- supporting multiple critical facilities simultaneously
- evaluating additional shortest path algorithms
- integrating dynamic or time-dependent network conditions
- developing an interactive visualization interface

---

## Motivation

This project was developed to explore how graph algorithms and geospatial data processing can be applied to a real-world transportation problem.

While the case study is based on the 2018 Kerala floods, the underlying workflow is applicable to any scenario that requires network accessibility analysis, shortest path computation, and infrastructure restoration planning.
