# SIT215 – Computational Intelligence  
## Assignment 3: Integrated Intelligent System

Hi, this repository contains my Assignment 3 project for SIT215.

The goal of this project was to build a delivery routing system in the Melbourne CBD by combining different AI techniques into one integrated system.

---

##  What this project does

The system finds a route from a starting location to a destination while also considering safety.

Instead of only finding the shortest path, it adjusts its behaviour based on:
- how fragile the cargo is  
- how rough the road is  
- whether conditions change during the trip  

---

##  How the system works

### 1. Baseline A* Search

I first built a basic A* route planner using a graph with 20 nodes.

Each node represents a location, and each edge represents a road.

- Constant speed: 100 km/h  
- Heuristic: straight-line distance  
- Resulting route:  
  `N1 → N3 → N5 → N10 → N9`

This gives a simple reference point before adding more realistic behaviour.

---

### 2. Fuzzy Logic (Safe Speed)

I then added a fuzzy system to calculate safe driving speed.

Inputs:
- Cargo fragility (low / medium / high)
- Road bumpiness (smooth / moderate / rough)

Output:
- Maximum safe speed (40–100 km/h)

Example:
- Fragility = 7, Bumpiness = 6  
→ Safe speed ≈ 50 km/h  

---

### 3. Integrated System

The fuzzy speed is combined with A*.

Instead of:

time = distance / 100


the system uses:

time = distance / fuzzy_safe_speed


This makes the route planning more realistic because speed is no longer fixed.

---

### 4. Replanning (Adaptive Behaviour)

To simulate real-world change, I added a school-zone condition.

- After 20% of the route  
- 60% of edges are limited to 40 km/h  

In my implementation, the change is triggered right after the initial route is calculated, so the system replans from N1.

The system then:
- updates speeds  
- recalculates the route  
- adapts to the new environment  

---

## 📊 What I observed

- The route often stays the same, but the travel time increases as cargo becomes more fragile  
- In some cases, replanning changes the path  
- In other cases, the path stays the same but becomes slower  

This shows that the system is adapting, not just following a fixed plan  

---

##  How to run

1. Open one of the notebooks depending on the task:

- Sit215task1.ipynb (Baseline A*)
- Sit215task2.ipynb (Fuzzy system)
- Sit215task3.ipynb (Integrated system)

2. Run all cells step by step

3. Check:
- route outputs  
- fuzzy speed results  
- replanning results  

2. Run all cells step by step

3. Check:
- route outputs  
- fuzzy speed results  
- replanning results  

---

##  Files in this repo

- `Sit215task1.ipynb` – baseline A* implementation  
- `Sit215task2.ipynb` – fuzzy logic system  
- `Sit215task3.ipynb` – integrated system with replanning  
- `Assignment3_Report.pdf` – final report  
- `README.md` – this file  
---
##  What I learned

This project helped me understand how different AI techniques can work together.

- A* handles planning  
- Fuzzy logic handles uncertainty  
- Replanning handles change  

Putting them together made the system more realistic compared to a simple baseline model.

---

##  Notes

- The 100 km/h speed is only used as a baseline for comparison  
- This is a simplified simulation, not a real traffic system  

---

Thanks for reading 🙂
All three tasks (baseline, fuzzy system, and integration) are included in this repository and can be run independently.
