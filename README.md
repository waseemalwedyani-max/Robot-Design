# Robot-Design
<img width="1600" height="905" alt="dog" src="https://github.com/user-attachments/assets/d0540a1c-81c0-4672-b680-82e68e5b5873" />
Source of the Picture https://www.printables.com/model/1443108-quadruped-i/files


Initial Mechanical Design and torque analysis for a Quadruped Robot - Smart Methods Summer Training 2026.
Welcome to the repository for the **Initial Mechanical Design of a Quadruped Robot**. This design was prepared as part of the 2026 summer training tasks for the (AI & Robotics / Mechanical Engineering) track. The project focuses on studying and analyzing the mechanical fundamentals that enable a robot to stand and walk stably.

---

## 📌 Table of Contents
1. [Body Shape and Structure](#1-body-shape-and-structure)
2. [Leg Design](#2-leg-design)
3. [Joints and Degrees of Freedom (DOF)](#3-joints-and-degrees-of-freedom-dof)
4. [Actuators and Motor Selection](#4-actuators-and-motor-selection)
5. [Initial Joint Torque Calculations](#5-initial-joint-torque-calculations)
6. [Stability and Center of Gravity (COG)](#6-stability-and-center-of-gravity-cog)
7. [Proposed Walking Gait](#7-proposed-walking-gait)
8. [Expected Mechanical Challenges and Solutions](#8-expected-mechanical-challenges-and-solutions)

---

## 1. Body Shape and Structure
* **General Design:** A flat, compact rectangular base (Chassis) designed to evenly distribute loads and provide ample space for mounting electronic components in the center.
* **Proposed Material:** Durable 3D-printed plastic (**PLA** or **PETG**) to minimize overall weight and allow for easy manufacturing/modification, or laser-cut acrylic sheets for rapid prototyping.
* **Weight Distribution:** Heavy components (such as the battery) are mounted at the lowest possible point in the center of the chassis to lower the Center of Gravity (COG) and increase stability.

## 2. Leg Design
The legs are designed using simplified biomimicry of quadrupedal animal locomotion. Each leg consists of two main links:
1. **Femur (Upper Link):** Connected directly to the robot's body, controlling forward/backward movement.
2. **Tibia (Lower Link):** Responsible for determining the robot's height and making contact with the ground.
* **Foot:** Equipped with flexible rubber ends to increase **useful friction** with surfaces and prevent slipping during movement.

## 3. Joints and Degrees of Freedom (DOF)
The robot features a balanced design that provides freedom of movement while keeping mechanical control simple:

| Element | Description |
| :--- | :--- |
| **Number of Legs** | 4 Legs |
| **Joints per Leg** | 2 Joints (Hip/Shoulder + Knee) |
| **DOF per Leg** | $2 \text{ DOF}$ |
| **Total Robot DOF** | $8 \text{ DOF}$ |

*This configuration gives the robot full capability to walk forward, backward, and turn at various angles.*

## 4. Actuators and Motor Selection
* **Selected Motor:** **MG996R** servo motors (or mechanical equivalents).
* **Reason for Selection:** 
  * They feature an internal metal gearbox providing **High Torque and Low Speed**.
  * They allow precise angular control via a built-in feedback system, eliminating the need for complex external mechanical power transmission systems.

## 5. Initial Joint Torque Calculations
To ensure the correct motor is chosen, the minimum required torque was calculated for the worst-case mechanical scenario (when the leg is fully extended horizontally):

### 🔹 Basic Assumptions:
* Total mass of the robot ($m$): $1.5 \text{ kg}$
* Length of the femur link ($r$): $0.1 \text{ m}$ (10 cm)
* Acceleration due to gravity ($g$): $9.81 \text{ m/s}^2$

### 🔹 Calculation Steps:
1. **Calculate the force due to the total weight of the robot:**
   $$F = m \times g = 1.5 \times 9.81 = 14.715 \text{ N}$$

2. **Load Analysis during Walking:**
   In a Trot Gait, the robot rests on two diagonal legs simultaneously, meaning each supporting leg carries about half the weight:
   $$F_{\text{leg}} = \frac{14.715}{2} = 7.357 \text{ N}$$

3. **Calculate Static Torque:**
   $$\tau = F_{\text{leg}} \times r = 7.357 \times 0.1 = 0.735 \text{ N.m}$$

4. **Apply Safety Factor:**
   To account for harmful friction, acceleration, and the weight of the legs themselves, the torque is multiplied by a safety factor ($SF = 2$):
   $$\tau_{\text{required}} = 0.735 \times 2 \approx 1.47 \text{ N.m}$$

Since the MG996R provides a torque between **1.1** and **1.3 N.m** at 6V (and can peak higher), it is an excellent and sufficient choice for operating the robot efficiently under normal conditions.

## 6. Stability and Center of Gravity (COG)
* **Center of Gravity:** Located exactly at the geometric center of the chassis to ensure equal load distribution across all four joints.
* **Static Stability Condition:** The control systems are designed so that the vertical projection of the COG always falls within the **Polygon of Support** formed by the feet touching the ground to prevent tipping over.

## 7. Proposed Walking Gait
Initially, the static **Creep Gait** is used to ensure maximum stability:
* **Movement Mechanism:** Only one leg is lifted and moved per step, while the other three legs remain grounded. This ensures the COG stays within the supporting triangle.
* **Movement Sequence:** Front-Right $\rightarrow$ Rear-Left $\rightarrow$ Front-Left $\rightarrow$ Rear-Right.

## 8. Expected Mechanical Challenges and Solutions

1. **Mechanical Backlash:** Small gaps between motor gears can cause leg jitter.
   * *Solution:* Use high-quality metal gear servos and reduce the length of the kinematic links to mitigate the lever effect.
2. **Motor Overheating (Holding Torque):** Exerting continuous torque to resist gravity while standing raises the motor temperature.
   * *Solution:* Program an "idle/rest state" to reduce applied effort when the robot is stationary, and design the chassis with mechanical angles that naturally support the structure.
3. **Harmful Joint Friction:** Bolting 3D-printed parts directly increases the load on the motor.
   * *Solution:* Integrate miniature bearings at pivot points to facilitate smooth movement and reduce power consumption.
4. **Chassis Bending:** The robot base bowing under the weight of the battery and electronic components.
   * *Solution:* Add longitudinal and transverse support ribs to the top and bottom of the base to increase structural rigidity.

