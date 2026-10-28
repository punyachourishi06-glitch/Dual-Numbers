# epfl-e3-prep

Two small learning projects I did while preparing my application to the EPFL
Excellence in Engineering (E3) research internship. Each one is a hands-on way
to understand an idea from research I read about. They are learning exercises,
not research results, and I am not affiliated with the labs mentioned.

## 1. `autodiff_dual_numbers/` - forward-mode automatic differentiation

**Inspired by:** Prof. Michael Herbst's talk "Algorithmic differentiation (AD)
for plane-wave DFT" (IPAM, 2025), and the related paper by Schmitz, Ploumhans
and Herbst (arXiv 2509.07785).

**The idea:** A material property such as a force or a band gap is a derivative
of some quantity with respect to a parameter. AD computes those derivatives
automatically by carrying a value and its derivative together through the
program (a "dual number") and applying the chain rule at every step.

**What I built:** `dual_numbers.py`, a small Python class from scratch, with:
- arithmetic rules (sum, product, quotient, power) and a custom rule for `exp`
- the lecture's example, f(x) = x^3 - x^2 at x = 2 (value 4, derivative 8)
- a check against a finite-difference estimate and a hand-derived derivative
- a toy "inverse design" loop that tunes a made-up strain until a made-up band
  gap reaches a target, using the derivatives from the dual numbers

**How to run:** `python dual_numbers.py` (plain Python, no installs).

**What I observed:** <!-- WRITE 2-3 SENTENCES IN YOUR OWN WORDS, e.g. what
happened when you tried the bumpy gap function, and whether the result matched
PyTorch or JAX autograd if you checked -->

**Limits:** This is not DFT. It is a toy model of the technique, and it only
handles a single input variable.

## 2. `pet_mad_silicon/` - trying a machine-learned interatomic potential

**Inspired by:** the COSMO lab's (Prof. Michele Ceriotti, EPFL) PET-MAD model,
described in Mazitov et al., "PET-MAD as a lightweight universal interatomic
potential for advanced materials modeling", Nature Communications (2025), and
the lab's open-source `upet` package (https://github.com/lab-cosmo/upet).

**The idea:** Simulating atoms with quantum mechanics is very expensive. A
machine-learned interatomic potential is trained on such calculations and then
predicts energies and forces almost instantly.

**What I did:** `pet_mad_silicon.py` uses the lab's published model, unmodified,
to:
1. compute the energy and forces of a perfect silicon crystal
2. displace the atoms slightly and let the model relax them (geometry optimization)
3. scan the lattice constant and compare the model's preferred value with
   the experimental value (about 5.43 angstrom)

**How to run:** `pip install upet ase numpy matplotlib`, then
`python pet_mad_silicon.py` (the first run downloads the model).

**Results:** <!-- FILL IN FROM YOUR OWN RUN: forces on the perfect crystal,
energy before and after relaxation, the model's lattice constant versus
experiment, and the plot si_lattice_scan.png -->

**What I found surprising or did not understand:** <!-- ONE OR TWO HONEST
SENTENCES -->

**Limits:** I used the model as a user. I did not train or modify it, and I
tested only one simple material.

## Environment
Python 3, run on Google Colab (CPU).
