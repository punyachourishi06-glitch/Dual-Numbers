# EPFL E3 Research Preparation

Two independent, research-inspired computational projects I developed while preparing my application to the EPFL Excellence in Engineering (E3) research internship.

Each project is a hands-on exploration of an idea from scientific research. My goal was to move beyond reading papers and lectures by implementing or testing the underlying methods myself.

These are learning exercises, not original research results. I am not affiliated with the laboratories or researchers mentioned.

## Projects

### 1. Forward-Mode Automatic Differentiation Using Dual Numbers

**Directory:** `autodiff_dual_numbers/`

**Inspired by:** Prof. Michael Herbst's talk, *Algorithmic Differentiation (AD) for Plane-Wave DFT* (IPAM, 2025), and the related paper by Schmitz, Ploumhans, and Herbst ([arXiv:2509.07785](https://arxiv.org/abs/2509.07785)).

#### Motivation

In computational physics, quantities such as forces and energy derivatives are essential for understanding and optimizing physical systems. Automatic differentiation (AD) provides a way to compute derivatives accurately by applying the chain rule through a sequence of computational operations.

I wanted to understand how this works at a fundamental level, rather than relying on an existing AD library.

#### What I implemented

In `dual_number.ipynb`, I implemented a lightweight forward-mode automatic differentiation system using dual numbers.

The notebook includes:

* A custom dual-number class carrying both a value and its derivative.
* Arithmetic operations: addition, subtraction, multiplication, division, and power.
* A custom implementation of the exponential function.
* The example from the lecture: \(f(x)=x^3-x^2\) evaluated at \(x=2\).
* Validation against an analytical derivative and a finite-difference estimate.
* A toy inverse-design optimization loop that adjusts a hypothetical strain to reach a target band gap using derivatives obtained through dual numbers.

#### What I learned

Implementing the arithmetic rules helped me understand how the chain rule can be applied automatically through a computational graph.

The inverse-design exercise also helped me connect differentiation to optimization: instead of searching blindly for a parameter, derivatives provide information about how to change it.

#### Limitations

This is a small educational implementation, not a plane-wave DFT calculation. It supports a single independent input variable and does not implement a complete scientific AD framework.

---

### 2. Exploring Machine-Learned Interatomic Potentials for Silicon

**Directory:** `pet_mad_silicon/`

**Inspired by:** The COSMO laboratory at EPFL, led by Prof. Michele Ceriotti, and the PET-MAD model described in:

Mazitov et al., *PET-MAD as a lightweight universal interatomic potential for advanced materials modeling*, Nature Communications (2025).

Model implementation: [lab-cosmo/upet](https://github.com/lab-cosmo/upet)

#### Motivation

Quantum-mechanical calculations can provide detailed information about atomic interactions, but they are computationally expensive.

Machine-learned interatomic potentials aim to approximate these interactions using models trained on quantum-mechanical calculations, allowing energies and forces to be evaluated much more efficiently.

I wanted to explore how such a model behaves on a simple material and understand how its predictions compare with experimental reference values.

#### What I did

In `pet_mad_silicon.ipynb`, I used the published PET-MAD model to investigate crystalline silicon.

The notebook explores:

1. Calculating the energy and forces of a perfect silicon crystal.
2. Perturbing the atomic positions and relaxing the structure using the model.
3. Scanning the lattice constant to investigate the model's preferred equilibrium value.
4. Comparing the calculated lattice constant with the experimental reference.

#### Results

The model produced the following results in my silicon test:

| Experiment                          | Observation                                              |
| ----------------------------------- | -------------------------------------------------------- |
| Perfect silicon crystal             | Near-zero forces, with a maximum magnitude of 0.007 eV/Å |
| Relaxation of a perturbed structure | Relaxed to the same energy in 13 optimization steps      |
| Preferred lattice constant          | 5.459 Å                                                  |
| Experimental reference              | Approximately 5.431 Å                                    |
| Relative difference                 | Approximately 0.5%                                       |

The model's preferred lattice constant was close to the experimental reference in this small test.

Seeing the model reproduce a physically meaningful quantity made the potential of machine-learned interatomic potentials for accelerating materials simulations more tangible to me.

#### Questions I want to explore further

The results also raised questions that I would like to understand more deeply:

* How can we determine when a machine-learned interatomic potential is reliable?
* What happens when the model encounters chemical environments that differ significantly from its training data?
* How can uncertainty estimates help identify predictions that should not be trusted?
* What physical principles and mathematical assumptions underlie these models?

These questions motivated my interest in the reliability and limitations of machine learning methods for scientific discovery.

#### Limitations

This was a small-scale test on crystalline silicon using a pretrained model.

I did not train or modify PET-MAD. The experiment does not establish the model's accuracy for other materials, chemical environments, or configurations outside its training distribution.

The comparison with the experimental lattice constant is a useful reference, but it is not a comprehensive validation of the model.

---

## Environment

* Python 3
* Jupyter Notebook
* Google Colab
* NumPy
* ASE (Atomic Simulation Environment)
* PET-MAD / `upet`

The automatic differentiation notebook uses plain Python and does not require an external AD library.

The PET-MAD notebook requires the model and its dependencies. The first execution may involve downloading the pretrained model.

## Acknowledgements

These projects were inspired by publicly available research papers, lectures, and open-source implementations.

I am grateful to the researchers whose work made these learning exercises possible.

The projects are independent educational explorations and are not affiliated with EPFL or the laboratories mentioned.


