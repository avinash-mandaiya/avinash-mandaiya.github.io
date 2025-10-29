---
layout: page
title: Protein Folding
description: Ab Initio Protein Folding via constraint-based optimization.
img: assets/img/balls_sticks.png
importance: 3
#category: fun
published: true 
---

<div class="row justify-content-center">
    <div class="col-sm-6 col-md-4 mt-3 mt-md-0">
        <video src="{{ '/assets/img/1LB0_new.mp4' | relative_url }}" class="img-fluid rounded z-depth-1" style="height: 400px; width: auto; object-fit: contain;" controls autoplay loop muted>
            Your browser does not support the video tag.
        </video>
    </div>
    <div class="col-sm-6 col-md-4 mt-3 mt-md-0">
        <video src="{{ '/assets/img/1UAO.mp4' | relative_url }}" class="img-fluid rounded z-depth-1" style="height: 400px; width: auto; object-fit: contain;" controls autoplay loop muted>
            Your browser does not support the video tag.
        </video>
    </div>
</div>
<div class="caption text-center">
    RRR runs demonstrating miniprotein folding via constraint-based optimization.
</div>


### Overview

The **protein folding problem** asks: given a primary amino-acid sequence and environment (temperature, ionic strength, pH, solvent), what 3D structure is thermodynamically favored? While learning-based models (e.g., AlphaFold2/3) are transformative, they rely heavily on **homology** and can struggle with **no-homologue sequences, novel mutations, intrinsically disordered regions,** and **highly dynamic proteins**. They also operate as “black boxes,” offering limited mechanistic insight for design.

### Ab Initio Approach

We take a **first-principles** route. Classical force fields (CHARMM/AMBER) model bonded terms (bond stretch, angle bend, dihedrals, impropers, Urey–Bradley) and non-bonded terms (electrostatics, van der Waals). Brute-force MD can capture folding, but long timescales (µs–ms) make it **computationally expensive** per system.

**Bonded terms are stiff** therefore they strongly constrain the local geometry. We treat much of the local structure as **geometric constraints** and focus search on **non-bonded interactions** and **dihedrals** while applying additional constraints via divide & concur framework that trims the search space.

### Constraint Satisfaction Formulation

We represent the structure with two variable types:
- **Positions:** atomic coordinates for enforcing **geometric constraints** (rigid motifs: peptide planarity, hybridization geometry, rigid fragments; and dihedral motif choices like gauche/anti with small tolerances).
- **Energies:** per-pair **Coulomb** and **van der Waals** contributions, plus a **global energy target**.

We solve via **divide–and–concur**:
- **Divide:** enforce constraints locally using **projections**  
  - *Energy consistency:* tie energy variables to the corresponding interatomic distances (Coulomb; modified LJ for tractable projection).  
  - *Geometry:* rigid-body projections (Kabsch–Umeyama) with **short-projection tolerances** (~0.1 Å) for realism.  
  - *Hydrogen bonding:* two constraints—(i) minimum total H-bonds, (ii) **secondary-structure units** (helix i→i−4, anti-parallel sheet pairings).  
- **Concur:** reconcile replicas into a **globally consistent** set of positions/energies and enforce a **total non-bonded energy threshold** (progressively lowered across runs).

The iteration uses **Reflect–Reflect–Relax (RRR)**:

$$
y' = y + \beta\big(P_B(2P_A(y) - y) - P_A(y)\big), \quad \beta \in (0,2)
$$


### Why This Helps

- **Efficiency:** Constraints prune vast swaths of implausible conformations without expensive dynamics.  
- **Extensibility:** New biophysical priors (e.g., H-bond counts, hydrophobic core compactness, residue-specific propensities) slot in as projections—no retraining required.  
- **Mechanistic clarity:** Each projection corresponds to a **physical rule**, yielding interpretable levers.

### Illustrative Results (Miniproteins)

Using modest H-bond counts and an energy target, the method recovers native-like folds for **helical** (e.g., 1LB0) and **β-sheet** (e.g., 1UAO) miniproteins with in tens of thousands of RRR iterations as shown in the figure below. A small explicit solvent shell is used; **water–water** interactions are disabled to avoid spurious clustering while retaining essential protein–water contacts.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1UAO.png" title="Folding via constraint satisfaction" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
	RRR run showing different stages of folding for 1UAO compared to the true fold.
</div>

### Takeaways

- Constraint-based folding is a **practical middle ground**: more mechanistic than pure ML and often far cheaper than long MD trajectories.  
- It’s a principled platform for **design and refinement**, where you can enforce what you know (geometry, hydrogen bonds, energies) and search efficiently for structures that satisfy those facts.

---



