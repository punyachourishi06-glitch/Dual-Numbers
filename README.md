# epfl-e3-prep

Two small learning projects I did while preparing my application to the EPFL Excellence in Engineering (E3) research internship. Each one is a hands-on way to understand an idea from research I read about. They are learning exercises, not research results, and I am not affiliated with the labs mentioned.

## 1. `autodiff_dual_numbers/` - forward-mode automatic differentiation

**Inspired by:** Prof. Michael Herbst's talk "Algorithmic differentiation (AD) for plane-wave DFT" (IPAM, 2025), and the related paper by Schmitz, Ploumhans and Herbst (arXiv 2509.07785).

**The idea:** A material property such as a force or a band gap is a derivative of some quantity with respect to a parameter. AD computes those derivatives automatically by carrying a value and its derivative together through the program (a "dual number") and applying the chain rule at every step.

**What I built:** `dual_number.ipynb`, a Jupyter notebook implementing a small Python class from scratch, with:
- Arithmetic rules (sum, product, quotient, power) and a custom rule for `exp`
- The lecture's example, f(x) = x³ − x² at x = 2 (value 4, derivative 8)
- A check against a finite-difference estimate and a hand-derived derivative
- A toy "inverse design" loop that tunes a made-up strain until a made-up band gap reaches a target, using derivatives from the dual numbers

**How to run:** Open `autodiff_dual_numbers/dual_number.ipynb` in Google Colab or Jupyter Notebook and run the cells in order. Plain Python is sufficient; no extra installations should be needed for this notebook.

**What I observed:** <!-- Replace this comment with 2–3 sentences describing your actual results, including what happened with the bumpy gap function and whether you checked the result against PyTorch or JAX autograd. -->

**Limits:** This is not DFT. It is a toy model of the technique, and it only handles a single input variable.

## 2. `pet_mad_silicon/` - trying a machine-learned interatomic potential

**Inspired by:** The COSMO lab's (Prof. Michele Ceriotti, EPFL) PET-MAD model, described in Mazitov et al., "PET-MAD as a lightweight universal interatomic potential for advanced materials modeling", Nature Communications (2025), and the lab's open-source `upet` package (https://github.com/lab-cosmo/upet).

**The idea:** Simulating atoms with quantum mechanics is very expensive. A machine-learned interatomic potential is trained on such calculations and then predicts energies and forces almost instantly.

**What I did:** `pet_mad_silicon.ipynb` is intended to use the lab's published model, unmodified, to:
1. Compute the energy and forces of a perfect silicon crystal
2. Displace the atoms slightly and let the model relax them (geometry optimization)
3. Scan the lattice constant and compare the model's preferred value with the experimental value (about 5.43 angstrom)

**How to run:** Open `pet_mad_silicon/pet_mad_silicon.ipynb` in Google Colab and run the cells in order. Install `upet`, `ase`, `numpy` and `matplotlib` if the notebook requires them. The first run may download the model.

**Results:** <!-- Fill this in only after running the notebook. Report the forces on the perfect crystal, energy before and after relaxation, the model's lattice constant versus experiment, and the plot saved as si_lattice_scan.png. -->

**What I found surprising or did not understand:** <!-- Add 1–2 honest sentences based on your actual run. -->

**Limits:** I used the model as a user. I did not train or modify it, and I tested only one simple material.

## Environment

Python 3, Google Colab (CPU).

