# 2-Axis Gantry Forklift System

**Senior Capstone (ME 190/191), California State University, Sacramento** · Fall 2025 · 2-person team 

![SolidWorks model](images/cad_model.png)

## Problem
Warehouse workers often move items heavier than 60 lb, or items stored at height, by hand. That causes strain, accidents, and slow workflow. We built a **10%-scale automated warehouse gantry forklift** that picks up palletized loads and moves them between shelves.

## Design constraints
| Requirement | Target |
|---|---|
| Scale | 10% of an average warehouse (10,000 to 25,000 ft² full scale) |
| Design load | 4 lb scaled pallet |
| X-axis speed | 2 in/s unloaded, 1 in/s loaded |
| Z-axis speed | 0.8 to 1.0 in/s |
| Budget | under $1,000 (≈ $900 spent) |

## Design
- **X-axis dual actuator:** A gantry plate rides on 4 V-wheel micro bearings in an aluminum C-beam. It is driven by a 15 mm × 8 mm lead screw from NEMA 23 stepper motors, through flexible couplings (6.35 to 8 mm), flange bearings, and lock nuts.
- **Z-axis linear lift:** A matching gantry plate and C-beam base, driven by a NEMA 23 stepper on a **rack-and-pinion** lift that carries a fabricated forklift tine.
- **Materials:** Aluminum extrusion was chosen for its strength, availability, and machinability at this scale.
- **Rescope:** We replaced the original belt-driven X-axis with lead-screw actuators to make it easier to build and reduce complexity.
- **CAD and analysis:** The design was modeled in **SolidWorks**. We checked bending stress, shear stress, von Mises and Tresca criteria, factor of safety, and deflection by hand and with **SolidWorks FEA**.

## Manufacturing
- Drilled M5 holes into the motor housings to match the frame's hex standoffs
- Hand-tapped threads into the aluminum extrusion ends for rigid joints
- Drilled the gantry plate, guided by the CAD layout, to mount the rack-and-pinion lift
- Drilled brackets, standoffs, and connector plates for bolts and lock nuts
- Cut and shaped the forklift tine from metal plate and smoothed its edges

![Frame build](images/build_frame.jpg)

## Testing and results
Testing used an Arduino motion control program. I reviewed, tested, and tuned the code.

| Test | Target | Result |
|---|---|---|
| X-axis speed | 2 in/s | Lead-screw whip appeared near 2 in/s. Stable at about 1.1 in/s. **Final operating speed 0.8 in/s** with smooth travel over the full track |
| Z-axis speed | 0.8 to 1.0 in/s | **0.5 in/s**, stable over the full height |
| Load lift | 4 lb | **Lifted the full 4 lb** with no slipping, stalling, or deformation |

**Finding:** The rack and spur gear could back-drive under heavier loads, letting the lift drop. The design did not account for holding torque.

## Proposed revisions
- Use a fully supported **ball screw** on the X-axis to remove whip and reach the 2 in/s goal
- Add **limit switches and homing sensors** for repeatable, safe motion
- Replace the Z-axis rack-and-pinion with a **linear actuator** to prevent back-driving
- Fix motor-mount hole locations in CAD before ordering parts

## Bill of materials
![BOM](images/bom_1.png)
![BOM continued](images/bom_2.png)

Main vendors were OpenBuilds (C-beam, gantry plates, V-wheels, and nut blocks), McMaster-Carr, OYOSTEPPER (NEMA 23 motors), and Accu (trapezoidal lead screws).
