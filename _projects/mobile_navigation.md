---
layout: page
title: Safe & Efficient Mobile Robot Navigation
description: Ph.D. research on hierarchical topology map based global path planning and a pedestrian-model-based local planner with a provable collision-free guarantee
img:
importance: 3
category: work
related_publications: true
---

**Ph.D. Dissertation, University of Waterloo**

My dissertation, *Safe and Efficient Navigation of a Mobile Robot: Path Planning Based on Hierarchical Topology Map and Motion Planning with Pedestrian Behavior Model*, addressed global path planning and pedestrian-aware local motion planning for mobile robots operating in human environments, with two main contributions.

**Global path planning: Hierarchical Topology Map with Explicit Corridor (HTM-EC)**
I developed a skeleton-based hierarchical graph method that extracts equidistant points from obstacles in an occupancy grid map to build a topological backbone, guaranteeing a feasible path is found if one exists ("completeness"). A second refinement stage discretizes the skeleton path into corridors and applies dynamic programming to optimize cost, incorporating allowable-speed constraints in narrow passages to produce time-optimal, safety-aware paths. Validated in simulation and on a real mobile robot with actual occupancy grid maps.

**Local motion planning: Collision Arc**
For the local, reactive layer, I built on a pedestrian behavioral model — which mimics how people navigate crowds by choosing the walking direction with the most free space — but that model alone gives no collision-free guarantee. I introduced the *collision arc (CA)*: the set of headings at the robot's preferred speed that lead to a future collision, obtained by mapping raw range measurements (e.g., LiDAR) onto the robot's velocity space and combining this with velocity-obstacle theory. Constraining the pedestrian model's direction choice to fall outside the CA is proven to yield a collision-free desired velocity. Because the method operates directly on raw range measurements with constant-size data, its computational complexity is O(1) regardless of the number or type of obstacles — compared to O(n) or O(n²) for velocity-obstacle-based methods that process each obstacle individually. Simulations validated far-sighted, non-freezing behavior on the "freezing robot problem" and on symmetric/asymmetric circular crossing scenarios with up to 10 agents.

**Outcomes**
- Han, J.W., Jeon, S., Kwon, H.J., "Hierarchical Topology Map with Explicit Corridor for Global Path Planning of Mobile Robots," *Intelligent Service Robotics*, 2023 — journal extension of the AIM 2019 conference paper
- The collision-arc-based local planner was presented at a conference; a journal manuscript is in preparation
- Also contributed as a co-author to a labmate-led paper on MPC-based path-following control for holonomic mobile robots, published in *Control Engineering Practice* (2023)

**Video**
- [Mobile Robot Path Planning With Allowable Speed For Safety](https://www.youtube.com/watch?v=oDTTdYcj_qA)
