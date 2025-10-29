---
layout: page
title: Resolving Tangling in Multi-Conformer Refinement via Iterative Projections
#description: Multi-Conformer Refinement
img: assets/img/resolution.png
importance: 2
related_publications: true
#category: work
#giscus_comments: true
---

The advent of advanced crystallographic techniques has shifted structural biology from static, single-conformer models toward probing protein dynamics. Extracting cooperative motions from temporally and spatially averaged electron density maps requires both high-resolution data and refinement algorithms capable of handling conformational heterogeneity. However, current refinement protocols often fail due to the **tangling phenomenon**, in which conformational states become improperly intertwined during optimization.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img src="{{ '/assets/img/L1_density.gif' | relative_url }}" alt="L1 density" class="img-fluid rounded z-depth-1" style="height: 400px; width: auto; object-fit: contain;">
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img src="{{ '/assets/img/L2_density.gif' | relative_url }}" alt="L2 density" class="img-fluid rounded z-depth-1" style="height: 400px; width: auto; object-fit: contain;">
    </div>
</div>
<div class="caption">
	Refinement results showing initial tangled states transitioning to resolved configurations via iterative projections.
</div>

## Our Approach

We present an automated refinement methodology based on **iterative projections** by utilizing the divide-and-concur framework. This approach enables seamless integration of geometric constraints with experimental density constraints derived from observed scattering amplitudes.

By allowing constraints to be satisfied independently in the divide constraint set and making them consistent in the cocur constraint, one can utilize the iterative projection method like RRR to effectively circumvents tangling artifacts and achieves robust refinement performance, even for models initialized with R-factors as high as 12%.

Just as iterative projections revolutionized phase retrieval in crystallography, we demonstrate that they can also address the optimization challenges in multi-conformational refinement. This work establishes a computational foundation for advancing crystallographic methodologies to resolve conformational heterogeneity and ultimately capture protein dynamics at atomic resolution.

<!--
## Publication
{% cite mandaiya2025refinement %}
-->
