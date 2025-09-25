# pcb_placement.py
"""
===========================================================
PCB Component Placement – Coding Assignment
===========================================================

📌 Overview
-----------
This script implements a constraint-aware placement algorithm
for PCB components on a 50×50 board. It satisfies all the hard
constraints defined in the assignment and produces a visualization.

🛠 Components
-------------
- USB Connector (5×5) → Must touch a board edge
- Microcontroller (5×5) → Can be placed anywhere
- Crystal (5×5) → Must be within 10 units of Microcontroller
- MikroBus1 (5×15) → Must touch a board edge
- MikroBus2 (5×15) → Must touch the opposite edge of MikroBus1 and be parallel

✅ Hard Constraints
-------------------
1. Edge placement (USB, MB1, MB2 must touch board edge)
2. MB1 and MB2 are parallel and on opposite edges
3. Crystal within 10 units of MCU center
4. No overlaps
5. All inside 50×50 board
6. Center of Mass (COM) within 2 units of (25,25)
7. MCU–Crystal line does not intersect USB keep-out zone (10×15 rectangle)

⚙️ Algorithm Approach
----------------------
1. Place MikroBus connectors on opposite edges.
2. Place USB on any board edge.
3. Try Microcontroller positions near board center.
4. Search Crystal positions near MCU (≤10 units).
5. Validate COM, overlaps, boundary, and keep-out.
6. Stop when first valid placement is found.

🖼 Output
---------
- A plot (`placement.png`) showing components, keep-out zone, and COM.
- Console prints component coordinates and validation results.

🚀 How to Run
-------------
1. Save this file as pcb_placement.py
2. Install matplotlib:  pip install matplotlib
3. Run:  python pcb_placement.py
4. Check output:
   - Terminal → placement details
   - Image → placement.png

📊 Performance
---------------
- Uses heuristic pruning and sampling for <2s runtime.
- Ensures all hard constraints are satisfied.

===========================================================
"""
