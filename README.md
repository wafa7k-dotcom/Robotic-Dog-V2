# Robotic Dog V2

## Project Overview

This repository documents **Mission 5 – Robotic Dog Design and Assembly**.

The task consists of two main parts:

1. Propose and document the design and algorithm of a **new robotic dog that is larger than the current robot**, including its mechanical design, motors, electronics, movement algorithm, and future improvements.
2. Assemble the provided robotic dog components in **Onshape** and create an **Exploded View** showing how the components are assembled.

---

# Part 1 — Proposed Larger Robotic Dog


## Design Objective

The goal of the future robotic dog is to create a larger and stronger version of the current prototype.

The larger design should provide:

* More internal space for electronics.
* More space for the battery and power system.
* Better cable management.
* Increased mechanical strength.
* Higher motor torque.
* Better stability during walking.
* Higher payload capacity.
* More freedom to add sensors and autonomous navigation systems.

The current CAD model is used as a reference, while the following design represents a **proposed future larger version**.

---

## Proposed Dimensions

Possible initial dimensions for the larger robot are:

| Component                  | Proposed Dimension |
| -------------------------- | -----------------: |
| Body length                |           35–45 cm |
| Body width                 |           18–25 cm |
| Body height                |           10–15 cm |
| Leg length                 |           20–30 cm |
| Number of legs             |                  4 |
| Motors per leg             |                  2 |
| Degrees of freedom per leg |              2 DOF |
| Total motors               |                  8 |

> These values are proposed design targets and are not the measured dimensions of the current CAD files. Final dimensions should be determined after calculating the robot weight, center of gravity, motor torque, and battery size.

---

# Mechanical Design

## Main Body

The body acts as the main structural frame of the robot.

It should contain:

* Main controller
* Battery
* Power distribution system
* Servo controller
* Sensors
* Communication modules
* Wiring

The body should be lightweight but mechanically strong.

Possible materials include:

* PETG
* ABS
* Aluminum
* Carbon-fiber reinforced materials

---

## Leg Design

The robot has four legs:

* Front Left
* Front Right
* Rear Left
* Rear Right

For the future larger design, each leg can use **2 Degrees of Freedom (2-DOF)**.

### Hip Joint

The hip motor controls forward and backward movement of the leg.

### Knee Joint

The knee motor controls bending and extension of the leg.

Therefore:

```text
4 Legs × 2 Motors = 8 Servo Motors
```

This configuration provides better control and walking ability than the current single-servo-per-leg prototype.

---

# Motor Selection

## Current Robot

The current V2 prototype uses:

**4 × Tower Pro SG90 Micro Servo Motors**

One servo is used for each leg.

The SG90 is suitable for lightweight prototypes and educational robotic mechanisms.

Official SG90 specifications include approximately:

| Specification     | Value                           |
| ----------------- | ------------------------------- |
| Weight            | 9 g                             |
| Operating voltage | 4.8 V                           |
| Stall torque      | 1.8 kg·cm at 4.8 V              |
| Gear type         | POM                             |
| Size              | approximately 23 × 12.2 × 29 mm |

---

## Future Larger Robot

The larger robotic dog will be heavier than the current prototype.

Therefore, the SG90 should **not automatically be used for the larger design**.

Higher-torque motors should be selected after calculating:

* Robot total weight
* Leg length
* Required joint torque
* Payload
* Safety factor
* Walking acceleration

Metal-gear high-torque servo motors would be more suitable for the larger robot.

The final motor model should be selected only after the required torque has been calculated.

---

# Electronics

A possible electronic architecture for the larger robot includes:

## Main Controller

**ESP32**

The ESP32 can provide:

* Wi-Fi
* Bluetooth
* PWM control
* Sensor communication
* Remote control
* Processing for basic walking algorithms

---

## Servo Controller

Because the future design may use eight or more motors, a dedicated PWM controller can be used.

Example:

**PCA9685 16-Channel PWM Servo Driver**

This allows multiple servo motors to be controlled without using a separate ESP32 PWM pin for every motor.

---

# Power System

The servo motors should use a suitable external power supply rather than relying directly on the controller board.

A possible power architecture is:

```text
Battery
   ↓
Voltage Regulator / BEC
   ↓
Servo Driver
   ↓
Servo Motors
```

The ESP32 and servo power system should share a common electrical ground.

Battery voltage, regulator capacity, and wiring must be selected according to the final motor current requirements.

---

# Sensors

The larger robot can later include:

* IMU
* Ultrasonic sensor
* Camera
* LiDAR
* Force sensors
* Distance sensors

An IMU can help measure:

* Robot orientation
* Acceleration
* Tilt
* Balance

---

# Robot Walking Algorithm

The robot walking algorithm coordinates the movement of the four legs.

## Basic Algorithm

```text
START

Initialize ESP32
Initialize servo controller
Initialize sensors

Move all legs to standing position

WHILE robot is powered:

    Read sensor data
    Check robot orientation

    IF obstacle is detected:
        Stop movement
        Select a new direction

    Lift Front Left Leg
    Move Front Left Leg forward
    Place Front Left Leg on the ground

    Lift Rear Right Leg
    Move Rear Right Leg forward
    Place Rear Right Leg on the ground

    Stabilize the robot

    Lift Front Right Leg
    Move Front Right Leg forward
    Place Front Right Leg on the ground

    Lift Rear Left Leg
    Move Rear Left Leg forward
    Place Rear Left Leg on the ground

    Stabilize the robot

    Repeat walking cycle

END WHILE

STOP
```

---

# Balance Algorithm

An IMU can continuously monitor the orientation of the robot.

```text
Read IMU data

IF robot tilts left:
    Adjust right-side legs

IF robot tilts right:
    Adjust left-side legs

IF robot tilts forward:
    Adjust rear legs

IF robot tilts backward:
    Adjust front legs
```

The goal is to keep the robot's center of gravity inside the support area created by the legs.

---

# Obstacle Avoidance Algorithm

A distance sensor can be installed at the front of the robot.

```text
Measure distance

IF distance > safe_distance:

    Continue moving forward

ELSE:

    Stop

    Measure left side
    Measure right side

    Select the direction with more free space

    Turn toward the selected direction

    Continue walking
```

---

# Part 2 — Robotic Dog V2 Mechanical Assembly

## Overview

<img width="563" height="341" alt="image" src="https://github.com/user-attachments/assets/4ed30cb9-b43a-4acc-a30a-2985d02fd63e" />

https://cad.onshape.com/documents/656a9da7c2f8ab7654c78345/w/6d374e7b9414a2acbe7f6daa/e/c3afc28a2117431c29dba934?renderMode=0&uiState=6a875b928aab1a2459e838b1

The second part of the task was to assemble the provided robotic dog CAD components using **Onshape**.

The current V2 design is larger than the previous/current robotic dog design and provides additional internal space for:

* Electronics
* PCB
* Wiring
* Controller
* Battery

The increased body size can also improve component organization and mechanical stability.

---

# Bill of Materials — BOM

| Part                | File                                |    Quantity | Function                                          |
| ------------------- | ----------------------------------- | ----------: | ------------------------------------------------- |
| Main body structure | `BodyV2.SLDPRT`                     |           1 | Main structural frame and electronics compartment |
| Body cover          | `BodyCoverV2.SLDPRT`                |           1 | Protects and closes the robot body                |
| Left leg            | `leftLeg.SLDPRT`                    |           2 | Front and rear left legs                          |
| Right leg           | `rightLeg.SLDPRT`                   |           2 | Front and rear right legs                         |
| SG90 servo          | `SG90 - Micro Servo 9g - Tower Pro` |           4 | Drives the four leg joints                        |
| Servo Horn          | SG90 servo horn component           |           4 | Transfers servo rotation to the leg mechanism     |
| Servo screw         | SG90 screw component                |           4 | Secures each servo horn                           |
| Cap screw           | `B18.3.4M - 3 x 0.5 x 12 SBHCS`     | As required | Mechanical fastening                              |

---

# Current V2 Leg Design

The current V2 robot uses:

```text
4 Legs
4 SG90 Servo Motors
1 Servo per Leg
1-DOF per Leg
```

Each servo provides forward/backward rotational motion at the leg joint.

The robot uses:

* `leftLeg` for the left side.
* `rightLeg` for the right side.

The parts are mirrored to create the four leg positions.

This reduces the number of unique CAD components required.

---

# Body and Cover Design

## BodyV2

`BodyV2` is the main structural frame.

It provides:

* Four servo mounting areas.
* Internal electronics space.
* Battery space.
* Controller space.
* Cable-routing space.
* Structural support for all four legs.

---

## BodyCoverV2

`BodyCoverV2` closes the upper section of the robot.

Its functions include:

* Protecting internal components.
* Completing the external shape.
* Preventing electronics from being exposed.
* Providing additional structural rigidity.

The cover is mechanically secured to the body using screws.

---

# SG90 Servo Motors

The current assembly uses four SG90 micro servo motors.

Each motor is installed near one leg joint.

The servo horn is mounted on the servo output shaft and transfers rotational motion to the leg mechanism.

The servo screw secures the horn to the servo shaft.

---

# Assembly Process

The robotic dog was assembled in Onshape using the following procedure:

1. Import the provided SolidWorks part files into Onshape.
2. Create a new Assembly.
3. Insert `BodyV2`.
4. Use the body as the main reference component.
5. Insert `BodyCoverV2`.
6. Insert two `leftLeg` instances.
7. Insert two `rightLeg` instances.
8. Position the four legs at the four corners.
9. Insert four SG90 servo motors.
10. Position each servo inside its mounting location.
11. Attach the servo horns to the four motors.
12. Install the servo horn screws.
13. Align the leg joints with the servo mechanisms.
14. Install the required structural screws.
15. Install the upper body cover.
16. Check the complete mechanical assembly.

---

# Onshape Mates Used

## Fastened Mate

Fastened Mates were used for components that should remain fixed relative to each other.

Examples include:

* Servo motor to frame
* Servo horn screw
* Body components
* Fixed mounting components

---

## Revolute Mate

Revolute Mates were used at rotating joints.

This allows rotation around a single joint axis while restricting other movement.

They were useful for representing the rotational motion of the robot legs.

---

# Final Assembly

The completed mechanical model includes:

* Main body
* Upper body cover
* Four legs
* Four SG90 servo motors
* Four servo horns
* Servo screws
* Structural mounting components

The final Onshape Assembly represents the mechanical structure of the V2 robotic dog.

---

# Exploded View Status

The task also required an **Exploded View** showing the relationship between all components.

The Exploded View feature in Onshape was opened and an attempt was made to create the required exploded assembly.

However, I was **not able to complete the Exploded View correctly**, because I had difficulty separating and arranging all of the components using the Onshape Exploded View tools.

Therefore:

**The complete mechanical Assembly was successfully created, while the Exploded View remains incomplete.**

The completed assembly and available CAD files are included in this repository.

---

# Intended Exploded View Arrangement

The intended Exploded View should approximately separate the components as follows:

```text
                    Body Cover

        Servo                    Servo

     Horn / Screw             Horn / Screw


Left Leg                          Right Leg


                    BodyV2


Left Leg                          Right Leg


        Servo                    Servo

     Horn / Screw             Horn / Screw
```

This arrangement would clearly demonstrate how the main components are connected.

---

# Future Improvements

Future improvements could include:

* Complete the Onshape Exploded View.
* Increase the robot's physical dimensions.
* Replace SG90 motors with higher-torque motors for a larger version.
* Increase each leg from 1-DOF to 2-DOF or more.
* Add an IMU for balance control.
* Add obstacle detection.
* Add autonomous walking.
* Add a camera or LiDAR.
* Improve cable management.
* Perform mechanical stress analysis.
* Calculate required motor torque before selecting the final actuators.
* Design custom 3D-printable parts.
* Simulate leg movement before manufacturing.

---

# Suggested Repository Structure

```text
Robotic-Dog-V2/
│
├── README.md
│
├── CAD/
│   ├── BodyV2.SLDPRT
│   ├── BodyCoverV2.SLDPRT
│   ├── leftLeg.SLDPRT
│   ├── rightLeg.SLDPRT
│   ├── SG90/
│   └── Screws/
│
├── Assembly/
│   └── Robot_Dog_V2_Assembly.step
│
└── Images/
    ├── final_assembly.png
    └── exploded_view_attempt.png
```

---

# Conclusion

Mission 5 included both the documentation of a future larger robotic dog and the mechanical assembly of the current V2 robot.

The current V2 robotic dog was successfully assembled in Onshape using:

* `BodyV2`
* `BodyCoverV2`
* Four legs
* Four SG90 servo motors
* Servo horns
* Servo screws
* Mechanical fasteners

The proposed future version expands the concept by using stronger actuators, additional degrees of freedom, better power management, sensors, and balance and walking algorithms.

The complete mechanical assembly was successfully created.

The Exploded View was attempted but could not be completed correctly and remains an area for future improvement.

---

## References

* Tower Pro — SG90 Micro Servo official specifications.
* Onshape Help — Assembly Mates.
* Onshape Help — Fastened Mate.
* Onshape Help — Revolute Mate.
* Onshape Help — Exploded Views.
