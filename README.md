# Robotic-Dog-V2
This repository documents the second version (V2) of the robotic dog design. This version was designed to be larger in size compared to the previous/current robotic dog design in the project,

# Robotic Dog V2 — Mechanical Design Documentation

## Overview

This repository documents the second version (V2) of the robotic dog design. This version was designed to be **larger in size** compared to the previous/current robotic dog design in the project, with the goals of:

- Providing more internal space to fit the PCB, wiring, and controller without crowding.
- Better airflow/space for component cooling and battery placement.
- Improved stability during movement through a wider base and relatively longer legs.

> **Note:** Exact dimensions (length/width/height in mm) live inside the SolidWorks (`.SLDPRT`) files themselves — it's best to fill these in after opening the files in SolidWorks or Onshape to confirm actual values rather than estimating them.

---

## Bill of Materials (BOM)

| Part | File | Qty | Function |
|---|---|---|---|
| Main body structure | `BodyV2.SLDPRT` | 1 | Houses all electronic components (board, battery, wiring) and forms the robot's backbone |
| Body cover | `BodyCoverV2.SLDPRT` | 1 | Closes the body from the top, protects internal components, and gives the final outer shape |
| Left leg | `leftLeg.SLDPRT` | 2 (front & rear) | Leg assembly on the left side |
| Right leg | `rightLeg.SLDPRT` | 2 (front & rear) | Leg assembly on the right side, mirrored from the left leg |
| SG90 servo | `SG90 - Micro Servo 9g - Tower Pro` (×4 instances) | 4 | Hip joint actuator for each leg — 1 degree of freedom (1-DOF) per leg |
| Cap screw | `B18.3.4M - 3 x 0.5 x 12 SBHCS` | per mounting point | Fastens legs to body and motors to frame (M3 × 12mm, Socket Button Head Cap Screw) |

**Total:** Body + Cover + 4 legs (2 left + 2 right) + 4 SG90 servos + M3×12 screw set.

---

## Leg Design

- Each leg has a single **SG90** servo mounted at the hip joint, giving each leg **1 degree of freedom (1-DOF)** — forward/backward swing motion only in this version.
- The legs are designed as a mirrored pair (`leftLeg` / `rightLeg`), so the same base geometry is used on both sides with the direction mirrored, reducing the number of unique designs needed to just two parts instead of four.
- The servo horn attaches directly to the leg joint via M3 screws, and the servo body sits inside a printed pocket within the leg structure itself to prevent rotation or vibration.

## Body & Cover Design

- `BodyV2` is the main load-bearing frame, and includes:
  - Four mounting points for the servos (one per leg) at the four corners.
  - Dedicated internal space for mounting the ESP32, electronic board, and battery.
  - Wire-routing openings between the body and the motors to keep wiring clear of moving parts.
- `BodyCoverV2` mounts on top of the body with M3×12 screws, forming the upper outer protection and giving the robot its final appearance.

## Actuators Used

**Tower Pro SG90 Micro Servo** (× 4, one motor per leg):

| Spec | Value |
|---|---|
| Weight | ~9 g |
| Operating voltage | 4.8–6 V |
| Torque | ~1.8 kg·cm @4.8V / ~2.5 kg·cm @6V |
| Speed | ~0.1 sec/60° @4.8V |
| Gear type | Plastic |
| Rotation range | ~180° |

> The SG90 was chosen for its small size and weight, suitable for a medium–large design, with low cost that allows using 4 units without a major increase in overall cost or robot weight.

---

## Assembly Steps

1. Mount the four SG90 servos into their pockets inside `BodyV2` and secure them with M3 screws.
2. Attach `leftLeg` and `rightLeg` to the servo horns at their four positions (front-left, front-right, rear-left, rear-right).
3. Route the servo wires through the dedicated openings inside `BodyV2` toward the electronics compartment.
4. Install the electronic board (ESP32 + circuit) and battery inside `BodyV2`.
5. Close the body by mounting `BodyCoverV2` on top of `BodyV2` and securing it with M3×12 screws.

---

## Next Step: Exploded View on Onshape

After importing/uploading the six parts (`BodyV2`, `BodyCoverV2`, `leftLeg`, `rightLeg`, 4× `SG90`, screws) to your Onshape account:

1. Create a new **Assembly** and insert all the parts into it.
2. Mate the parts together using **Mates** (Fastened/Revolute depending on the connection type), following the same order as the assembly steps above.
3. From the Assembly menu, select the **Exploded View** feature.
4. Drag each part (or group of parts) away from its original position in a logical order (body in the center, legs spreading out to the sides, cover lifting upward, motors and screws shown separately).
5. Save the Exploded View and export it as a PNG image to add to this file or upload to the same repository.

---

## Suggested Repository Structure

```
V2DogDesign/
├── README.md                 
├── cad/
│   ├── BodyV2.SLDPRT
│   ├── BodyCoverV2.SLDPRT
│   ├── leftLeg.SLDPRT
│   ├── rightLeg.SLDPRT
│   ├── SG90.SLDPRT
│   └── screws/
└── exploded-view/
    └── exploded_view.png      ← the image exported from Onshape
```
