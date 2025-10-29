---
layout: page
title: Hexein Folding
description: A minimal lattice model that captures protein folding through constraint-based rules and iterative projections. 
img: assets/img/glob_hexein.png
importance: 4
#category: fun
published: true 
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/b29_chain.png" title="bowt29 sequence" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <em>bowt29</em> hexein's primary sequence.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/img/newb29err.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    Simulation depicting the RRR run and gap between divide and concur constraint sets that successfully folds <em>bowt29</em> hexein.
</div>

### Overview

**Hexein Folding** is a simplified two-dimensional model of protein folding that captures how hydrophobic and polar residues self-organize on a **hexagonal lattice**. Each residue is represented by a colored tile—hydrophobic (red), polar (blue), and solvent (cyan)—allowing the essential physics of **hydrophobic collapse** and **core–shell formation** to be studied in a computationally tractable way.

---

### Concept

Unlike traditional energy-minimization methods, Hexein treats folding as a **constraint satisfaction problem**. The system is defined by two empirical adjacency rules:

1. Hydrophobic residues (**H**) cannot contact solvent (**S**).  
2. Polar residues (**P**) must border both solvent and hydrophobic residues, forming a protective ribbon around the hydrophobic core.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/motifs27.png" title="Motifs" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
	Local configurations that satisfy adjacency rules are captured in a compact <b>motif library</b> of allowed 7-tile patterns. Each lattice site and its neighbors must match one of these motifs, drastically reducing the conformational search space.
</div>

---

### Method

Hexein Folding utilizes the **Reflect–Reflect–Relax (RRR)** algorithm within the **divide-and-concur** framework, a projection-based approach for solving non-convex constraint systems.  
- The *divide* constraint independtly  enforces local constraints (motifs, sequence order) and residue–lattice matching by creating replica variabes.  
- The *concur* constraint reconciles all replicas into a globally consistent fold.  

Projections are computed analytically or via efficient combinatorial optimization, such as the **Hungarian algorithm** for enforcing perfect matchings between residues and lattice sites.

---

### Insights

Even with simple binary sequences, Hexein exhibits key features of real protein folding:
- Hydrophobic collapse into a compact core.
- Solvent shielding by polar residues.
- Only a small fraction of sequences fold into unique, stable structures, reflecting the selective nature of functional proteins.

This proof-of-concept study makes Hexein folding helps in explaing and further exploration of constraint-based  algorithmic frameworks like RRR can be utilized to capture emergent structure in biological systems.

---

### Learn More

- **Write-up:** Thesis (coming soon)
- **Code:** [GitHub Repository](https://github.com/avinash-mandaiya/hexein_folding)

---


