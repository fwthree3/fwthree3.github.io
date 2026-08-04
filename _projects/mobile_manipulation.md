---
layout: page
title: Mobile Manipulator Demo at Pack EXPO
description: Autonomous pick-and-place and teach-and-play knob operation with a 7-DOF WAM arm on a mobile base, demonstrated live at Pack EXPO's Robotics Zone
img:
importance: 2
category: work
related_publications: false
---

**Ph.D. research demo, University of Waterloo — Robotics Zone, Pack EXPO (Las Vegas)**

I integrated a 7-DOF Barrett WAM arm onto a Summit_XLS mobile base to build a mobile manipulator, then took full responsibility for the task autonomy behind a live demo in the Robotics Zone at Pack EXPO. The system had to navigate between two tables, pick and place a bottle using vision-based grasping, and tighten/release a knob on a Septimatech guide-rail mockup — all within a compressed two-month development window.

**System architecture**
- `core_service_expo`: the central task controller, run on a laptop networked with the mobile base (Summit_XLS) and the WAM's controller over ROS
- `WAM_ik_solver`: a custom 7-DOF inverse kinematics service for the WAM
- Navigation via ROS `move_base` on the Summit_XLS; manipulation via `wam_node` talking to the WAM controller
- Vision via `aruco_single` nodes for object and robot pose estimation

**Task controller**
The 11-step task sequence (move → pick → move → place → move → tighten knob → release knob → move → pick → move → place) was driven by a single mode-based state machine: each mode issues either a target pose (navigation) or a joint command (manipulation) as a ROS service call, waits for completion, then advances — a simple, robust pattern for sequencing heterogeneous subsystems.

**Choosing a vision method**
I evaluated three pose-estimation approaches for the target object — DOPE (deep-learning, shape-based, requires a trained model), ArUco markers, and WHYCON (marker-based) — and ran a controlled accuracy comparison against a VICON motion-capture reference across 5 locations × 4 sub-locations on a calibrated 2D stage. DOPE proved sensitive to lighting and failed outright at one location, so I selected ArUco for the demo's reliability.

**7-DOF inverse kinematics for the WAM**
The WAM arm (3-DOF shoulder, 1-DOF elbow, 3-DOF wrist) is kinematically redundant, so I resolved the extra DOF by fixing the elbow (J4) position — either at the point closest to its current location or on the plane spanned by the J1–J7 and J7–Jtool lines — before solving the rest in closed form. When no solution existed for the commanded grasp orientation, the solver fell back to trying alternate approach angles about the object's z-axis (9 angles × 2 sides); this modification raised the solver's success rate to about 90% over 50,000 randomized test poses.

**Contributions**
- Full ownership of task autonomy for the live demo, including the mode-based task controller
- Custom 7-DOF IK solver for the WAM, with a multi-angle fallback strategy for infeasible orientations
- Jacobian-based trajectory planning for the manipulator
- Vision method selection based on a controlled accuracy experiment (ArUco over DOPE/WHYCON)
- Teach-and-play motion for the knob-tightening task

**Outcomes**: successfully demonstrated live at Pack EXPO's Robotics Zone (North Hall). Remaining issues noted afterward were mobile-base localization drift and short-range blind spots, manipulation performance bound by the WAM's internal controller, and the need for more robust vision under varied lighting.
