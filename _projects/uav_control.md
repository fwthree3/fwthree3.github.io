---
layout: page
title: UAV Safety Algorithm & Circular Path Tracking
description: Flight control safety unit and circular-path tracking algorithm for a fixed-wing UAV
img: assets/img/uav_control.jpg
importance: 1
category: miscellaneous
related_publications: false
---

**Graduate Research Assistant, Yonsei University**

I developed the circular-path tracking algorithm and the safety algorithm/circuit for a fixed-wing UAV's flight control system.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/uav_control_pcb.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**Contributions**
- Circular path tracking algorithm for the UAV
- Safety unit design: a control-transfer circuit that switches actuator commands between the flight control computer (FCC) and the R/C receiver (including fail-safe) if the FCC fails
- Partial responsibility for the overall UAV system

**Tools**: Code Composer (TI DSP compiler), AVR (ATMEGA compiler)
