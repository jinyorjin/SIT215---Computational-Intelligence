# SIT215 – Computational Intelligence

## Assignment 3: Integrated Intelligent System

Hi, this repository contains my Assignment 3 project for SIT215.

The goal of this project was to build a delivery routing system in the Melbourne CBD by combining different AI techniques into one integrated system.

---

## What this project does

The system finds a route from a starting location to a destination while also considering safety.

Instead of only finding the shortest path, it adjusts its behaviour based on:

- how fragile the cargo is
- how rough the road is
- whether conditions change during the trip

The project combines:

- A* search for route planning
- Fuzzy logic for safe speed calculation
- Replanning for changed road conditions

---

## How the system works

### 1. Baseline A* Search

I first built a basic A* route planner using a graph with 20 nodes and 37 edges.

Each node represents a Melbourne CBD location, and each edge represents a road segment.

- Constant speed: 100 km/h
- Heuristic: straight-line distance
- Resulting route: `N1 → N3 → N5 → N10 → N9`

This gives a simple reference point before adding more realistic behaviour.

---

### 2. Fuzzy Logic: Safe Speed

I then added a fuzzy system to calculate safe driving speed.

Inputs:

- Cargo fragility: low, medium, high
- Road bumpiness: smooth, moderate, rough

Output:

- Maximum safe speed: 40–100 km/h

Example:

- Fragility = 7
- Bumpiness = 6
- Safe speed ≈ 50.71 km/h

---

### 3. Integrated System

The fuzzy safe speed is combined with A* search.

Instead of using a fixed speed:

`time = distance / 100`

the integrated system uses:

`time = distance / fuzzy_safe_speed`

This makes the route planning more realistic because speed is no longer fixed. The route cost changes depending on cargo fragility and road bumpiness.

---

### 4. Replanning: Adaptive Behaviour

To simulate a real-world change, I added a school-zone condition.

- After 20% of the route
- 60% of graph edges are limited to 40 km/h

In my implementation, the change is triggered right after the initial route is calculated, so the system replans from N1.

The system then:

- updates safe speeds
- recalculates the route
- adapts to the changed environment

---

## What I observed

- The route often stays the same, but the travel time increases as cargo becomes more fragile.
- In some cases, replanning changes the path.
- In other cases, the path stays the same but becomes slower.

This shows that the system is adapting, not just following a fixed plan.

---

## Requirements

This project uses Python 3 and the following libraries:

`pip install numpy pandas matplotlib networkx`

Jupyter Notebook is also required to run the `.ipynb` file.

---

## How to run

1. Open the notebook:

`SIT215_Assignment3_Notebook_JinKim.ipynb`

2. Run all cells from top to bottom.

3. Check the outputs for:

- baseline A* route
- fuzzy safe speed result
- integrated A* comparison
- school-zone replanning result

---

## Files in this repo

- Notebook file – includes baseline A*, fuzzy logic, integration, and replanning
- Final report PDF – contains the full written report
- README.md – this file

---

## What I learned

This project helped me understand how different AI techniques can work together.

- A* handles route planning.
- Fuzzy logic handles uncertainty.
- Replanning handles environmental change.

Putting them together made the system more realistic compared to a simple baseline model.

---

## Notes

- The 100 km/h speed is only used as a baseline for comparison.
- This is a simplified simulation, not a real traffic system.
- The school-zone replanning condition is simulated for assignment purposes.

---

Thanks for reading.
