# SMARTFLOW: Intelligent Traffic Light Management System
## FDS Mini Project — Technical Report & Presentation Notes

**Course**: Fundamental of Data Structures (FDS)  
**Project Domain**: Traffic Management Simulation & Educational Data Structures  
**Platform**: Single-Page Web Application (React, TypeScript, Tailwind CSS, SVG, Vitest)

---

## 1. Problem Statement & Motivation

Traditional traffic signal lights operate on fixed timers regardless of how many cars are waiting at each approach. This leads to empty roads receiving green lights while packed roads suffer long delays.

**SMARTFLOW** demonstrates a congestion-aware traffic control model using three foundational computer science concepts:
1. **FIFO Queues** to maintain orderly vehicle departure.
2. **Lane Priority Selection** based on waiting traffic count.
3. **Bubble Sort** to rank all lanes from highest to lowest traffic.

---

## 2. Fundamental Data Structures & Algorithms

### 2.1 FIFO Queue (`FIFOQueue<T>`)
- **Structure**: Circular array buffer with `head` and `tail` pointers.
- **Operations**:
  - `enqueue(vehicle)`: Appends an incoming car to the **REAR** of the lane ($O(1)$).
  - `dequeue()`: Releases the front car when the signal is green ($O(1)$).
  - `peek()`: Inspects the vehicle currently at the stop line ($O(1)$).
- **Invariant**: Strict First-In, First-Out order. Vehicles leave in the exact sequence of their arrival.

### 2.2 Lane Priority Selection
- The system checks the number of waiting vehicles in each lane:
  - North: 2
  - South: 3
  - East: 4
  - West: 1
- **Selection Rule**: The lane with the maximum count (**EAST with 4 vehicles**) is selected as the priority candidate.

### 2.3 Bubble Sort (`BubbleSort`)
- **Purpose**: Educational sorting of four lane counts in descending order (highest to lowest).
- **Mechanism**:
  - Adjacent elements $[j]$ and $[j+1]$ are compared.
  - If the left element is smaller than the right element, they are swapped.
  - An early exit flag terminates sorting in $O(n)$ time when no swaps occur in a pass.
- **Complexity**:
  - Worst Case: $O(n^2)$ comparisons and swaps.
  - Best Case: $O(n)$ with early termination.
  - Space: $O(1)$ auxiliary storage.

### 2.4 Signal Safety Rules
- Signals operate in two non-conflicting movement groups:
  - **NORTH–SOUTH (NS)**
  - **EAST–WEST (EW)**
- Alternating sequence: `GREEN → YELLOW → OPPOSITE GREEN → OPPOSITE YELLOW → REPEAT`.
- Opposing flows never receive green lights simultaneously.

---

## 3. Presentation Walkthrough Steps

During evaluation, present the system using this 8-step narrative:
1. **Step 1 — Vehicles Arrive**: Vehicles join the rear of their lane queue.
2. **Step 2 — FIFO Queue**: Vehicles leave in the same order they arrived.
3. **Step 3 — Check Lane Counts**: The system reads queue sizes across all 4 lanes.
4. **Step 4 — Bubble Sort**: Adjacent counts are compared and sorted from highest to lowest.
5. **Step 5 — Select a Lane**: The lane with the highest count (e.g. East: 4) becomes the priority candidate.
6. **Step 6 — Traffic Signal**: The East-West group turns green while North-South waits at red.
7. **Step 7 — Vehicles Move**: The front car discharges and crosses smoothly.
8. **Step 8 — Repeat**: Updated queue counts are checked again.

---

## 4. Test Suite Summary

All 9 unit tests pass under Vitest (`npm test`):
- FIFO Queue ordering, capacity enforcement, and dequeue.
- Bubble Sort descending sort accuracy and early-exit optimization.
- Traffic Signal phase alternation with zero conflicting greens.
- Initial deterministic 10-car setup and Add Car operation.
- Complete reset verification.
