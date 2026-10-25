# SMARTFLOW — Smart Traffic Light Management System
### First-Year Engineering | Fundamental of Data Structures (FDS) Mini Project

> **A clean, beautiful, slow-animated traffic simulation dashboard designed for clear classroom explanation of FIFO Queues, Lane-Count Priority Selection, and Bubble Sort.**

---

## 1. Project Concept & Presentation Flow

In traditional fixed-timer traffic lights, each road gets the exact same green time regardless of how many cars are waiting. 

**SMARTFLOW** demonstrates an intelligent approach using Fundamental Data Structures:
```
VEHICLES ARRIVE 
  → JOIN A FIFO QUEUE 
  → TRAFFIC IS COUNTED 
  → COUNTS ARE SORTED (BUBBLE SORT) 
  → A LANE IS SELECTED (LANE PRIORITY) 
  → ITS SIGNAL TURNS GREEN 
  → THE FRONT VEHICLE MOVES 
  → THE PROCESS REPEATS
```

---

## 2. Core Data Structures & Concepts

### 1. FIFO Queue (`src/simulation/Queue.ts`)
* **Concept**: First-In, First-Out queue for each approach lane (North, South, East, West).
* **Rule**:
  - New incoming vehicles join at the **REAR**.
  - When the light is green, the front-most vehicle leaves from the **FRONT**.
* **Invariant**: Strict arrival order is preserved. No vehicle jumps ahead.

### 2. Lane Priority Selection (`src/components/LanePriorityPanel.tsx`)
* **Concept**: The system inspects how many vehicles are waiting in each lane:
  - North: 2 vehicles
  - South: 3 vehicles
  - East: 4 vehicles
  - West: 1 vehicle
* **Selection**: The lane with the highest waiting count (**EAST — 4 vehicles**) is selected as the priority candidate.

### 3. Bubble Sort (`src/simulation/BubbleSort.ts`)
* **Concept**: An adjacent pairwise comparison sort that ranks the four lane counts from highest to lowest traffic.
* **Demonstration**:
  - Highlights the two adjacent lanes currently being compared.
  - Swaps them if the left count is smaller than the right count (descending order).
  - Stops early ($O(n)$) when all lanes are in order.
  - Provides **Next Comparison**, **Play**, **Pause**, and **Reset** controls.

### 4. Simple Traffic Signal Coordination
* Alternates fairly between two movement groups:
  - **NORTH–SOUTH**
  - **EAST–WEST**
* Sequence: `GREEN → YELLOW → OPPOSITE GREEN → OPPOSITE YELLOW → REPEAT`.
* Conflicting directions never receive green at the same time.

---

## 3. Dashboard Sections

1. **Header**:
   - SMARTFLOW title, Start / Pause button, Reset button, and **SLOW (Default) / NORMAL** speed toggle.
2. **Animated Traffic Intersection (Centerpiece)**:
   - Deep navy asphalt, crisp road markings, traffic signals, and top-down vector vehicle illustrations (Cars and Bikes with visible wheels, windows, and headlights).
   - Clickable lane indicators and an **ADD CAR** button to test queue arrivals.
3. **How SmartFlow Works (Step-by-Step Walkthrough)**:
   - Explains the system step-by-step (`STEP 1 OF 8` to `STEP 8 OF 8`) with **Previous**, **Next Step**, **Auto Play**, and **Restart** controls.
4. **Which Lane Has More Traffic? (Lane Priority)**:
   - Four clean horizontal bars highlighting the lane with the highest waiting traffic.
5. **Bubble Sort — Lane Count Ranking**:
   - Visual comparison and swapping of the four lane counts.
6. **Vehicle Queue (FIFO Queue Inspector)**:
   - Real-time conveyor visualization showing `FRONT → Car 1 → Car 2 → REAR`.

---

## 4. Setup & Running Locally

```bash
# 1. Install dependencies
npm install

# 2. Start local development server
npm run dev

# 3. Run unit tests
npm test

# 4. Build for production
npm run build
```

Open your browser to:
```
http://localhost:5173/
```
The clean, single-page dashboard appears immediately.
