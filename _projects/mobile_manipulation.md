---
layout: page
title: Mobile Manipulator
description: Autonomous pick-and-place and teach-and-play knob operation with a 7-DOF WAM arm on a mobile base, demonstrated live at Pack EXPO's Robotics Zone
img: assets/img/mobile_manipulation_knob.jpg
importance: 2
category: work
related_publications: false
---

**Ph.D. research demo, University of Waterloo — Robotics Zone, Pack EXPO (Las Vegas)**

I integrated a 7-DOF Barrett WAM arm onto a Summit_XLS mobile base to build a mobile manipulator, then took full responsibility for the task autonomy behind a live demo in the Robotics Zone at Pack EXPO. The system had to navigate between two tables, pick and place a bottle using vision-based grasping, and tighten/release a knob on a Septimatech guide-rail mockup — all within a compressed two-month development window.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/mobile_manipulation.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**System overview**
The system networked three subsystems over ROS: a laptop running the central task controller and vision processing, the mobile base handling navigation, and the WAM arm handling manipulation. An 11-step task sequence (move → pick → move → place → move → tighten knob → release knob → move → pick → move → place) was driven by a simple mode-based state machine, where each step issued either a navigation target or a manipulation command and waited for completion before advancing.

**Choosing a vision method**
I evaluated three pose-estimation approaches for the target object — DOPE (deep-learning, shape-based, requires a trained model), ArUco markers, and WHYCON (marker-based) — and ran a controlled accuracy comparison against a VICON motion-capture reference across 5 locations × 4 sub-locations on a calibrated 2D stage. DOPE proved sensitive to lighting and failed outright at one location, so I selected ArUco for the demo's reliability.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/mobile_manipulation_vision.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**7-DOF inverse kinematics for the WAM**
The WAM arm (3-DOF shoulder, 1-DOF elbow, 3-DOF wrist) is kinematically redundant, so I resolved the extra DOF by fixing the elbow (J4) position — either at the point closest to its current location or on the plane spanned by the J1–J7 and J7–Jtool lines — before solving the rest in closed form. When no solution existed for the commanded grasp orientation, the solver fell back to trying alternate approach angles about the object's z-axis (9 angles × 2 sides); this modification raised the solver's success rate to about 90% over 50,000 randomized test poses.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/mobile_manipulation_wam_kinematics.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**Contributions**
- Full ownership of task autonomy for the live demo, including the mode-based task controller
- Custom 7-DOF IK solver for the WAM, with a multi-angle fallback strategy for infeasible orientations
- Jacobian-based trajectory planning for the manipulator
- Vision method selection based on a controlled accuracy experiment (ArUco over DOPE/WHYCON)
- Teach-and-play motion for the knob-tightening task

**Outcomes**: successfully demonstrated live at Pack EXPO's Robotics Zone (North Hall). Remaining issues noted afterward were mobile-base localization drift and short-range blind spots, manipulation performance bound by the WAM's internal controller, and the need for more robust vision under varied lighting.

**Videos**
- [Mobile Manipulator Multi-Floor Operation](https://www.youtube.com/watch?v=rkKu2eE83Ss)
- [NMPC Pick and Place](https://www.youtube.com/watch?v=KnoEmmT15cc)
- [Advanced Robotics Research at the University of Waterloo's RoboHub](https://www.youtube.com/watch?v=eBBXOahmkuU)
