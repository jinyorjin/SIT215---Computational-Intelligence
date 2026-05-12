# SIT215 – Computational Intelligence

## Assignment 3: Integrated Intelligent System Project

Hi, this repository contains my SIT215 Assignment 3 project.

This project implements an integrated intelligent delivery-routing system for the Melbourne CBD. The system combines A* search, fuzzy logic, and reactive replanning to find a route while also considering cargo safety and changed road conditions.

---

## Project Overview

The goal of this project is to find the fastest route from a start node to a goal node in a road-network graph.

However, instead of only using physical distance, the system also considers:

- cargo fragility
- road bumpiness
- school-zone speed constraints
- replanning when the environment changes

The project combines three main computational intelligence components:

- **A* search** for route planning
- **Fuzzy logic** for maximum safe-speed calculation
- **Reactive replanning** for changed environmental conditions

---

## 1. Baseline A* Search

The first part of the project implements a baseline A* route planner.

The environment is represented as a Melbourne CBD graph with:

- 20 nodes
- 37 edges
- real-world distance values between connected locations

In the baseline model, every road segment uses a constant speed of **100 km/h**. This is not intended to represent a real Melbourne CBD speed limit. It is used as a controlled comparison point before fuzzy logic is added.

Baseline result:

```text
Route: N1 → N3 → N5 → N10 → N9
Total distance: 0.990 km
Total time: 0.594 minutes
2. Fuzzy Logic System

The fuzzy inference system calculates the maximum safe speed for each road segment.

Inputs:

Cargo fragility: low, medium, high
Road bumpiness: smooth, moderate, rough

Output:

Maximum safe speed between 40 km/h and 100 km/h

Representative example:

Cargo fragility = 7
Road bumpiness = 6
Safe speed ≈ 50.71 km/h

The rule base follows a safety-focused idea: as fragility or bumpiness increases, the safe speed decreases.

3. Integrated A* System

The fuzzy safe speed is then integrated into A* search.

Instead of using the baseline cost:

time = distance / 100

the integrated system uses:

time = distance / fuzzy_safe_speed

This allows the route cost to change depending on cargo fragility and road bumpiness.

The route may remain the same, but the travel time increases when the cargo becomes more fragile. This shows that fuzzy logic affects the internal travel-time cost, even when the visible route does not change.

4. Reactive Replanning

To simulate a changed road environment, the project adds a school-zone constraint.

In this scenario:

the original route is first planned
after 20% of the route is reached, the environment changes
60% of graph edges are selected as school-zone constrained edges
constrained edges are capped at 40 km/h
A* replans from the current node using the updated edge costs

A fixed random seed is used so that the constrained edges are reproducible.

In this implementation, the original route is short, so the 20% trigger occurs very early and replanning starts from N1. This is treated as an early-route replanning test.

Key Observations

The results show that:

the baseline A* system provides a useful reference route
fuzzy logic increases travel time as cargo fragility increases
replanning can change the selected path under school-zone constraints
in some cases, the path stays the same but the travel time increases
the system adapts to changed conditions instead of following a fixed original plan

Overall, the integrated system is more safety-aware than the baseline model because it considers both route efficiency and delivery risk.

Requirements

This project uses Python 3.

Required libraries:

pip install numpy pandas matplotlib networkx

The project is designed to run in Jupyter Notebook.

How to Run the Project
Open the notebook file:
SIT215_Assignment3_Notebook_JinKim.ipynb
Run all cells from top to bottom.
Review the outputs for:
baseline A* route
fuzzy membership functions
defuzzification example
integrated A* comparison
edge safe-speed examples
school-zone replanning results
route visualisations and flowchart
Files in This Repository
SIT215_Assignment3_Notebook_JinKim.ipynb
README.md
Final report PDF

The notebook includes the full implementation for:

graph environment construction
baseline A* search
fuzzy inference system
integrated A* planning
school-zone replanning
tables and figures used in the report
Notes
The 100 km/h speed is used only as a baseline comparison value.
The bumpiness values are modelling estimates based on the original Assignment 1 edge costs.
The school-zone constraint is simulated for assignment purposes.
This project is a simplified intelligent-routing model, not a real traffic-management system.
Acknowledgement

This project reuses and extends my previous SIT215 Assignment 1 graph model and Assignment 2 fuzzy logic design. I adapted them for Assignment 3 by adding distance-based A* search, fuzzy safe-speed calculation, integrated route planning, and reactive replanning.
