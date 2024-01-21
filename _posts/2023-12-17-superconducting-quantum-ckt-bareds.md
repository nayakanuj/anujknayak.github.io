---
title: 'Understanding high-fidelity supercoducting universal quantum gates'
date: 2024-01-21
permalink: /posts/2023/12/xmon_barends/
tags:
  - Xmon, Transmon
  - Superconducting quantum circuits
  - Fast-adiabatic C-Z gate
  - Surface code threshold
  - High fidelity
---

This post is a summary of the paper ``[Supercoducting quantum circuits at the surface code threshold for fault tolerance](https://www.nature.com/articles/nature13171)" by Barends et al. The goal of this blogpost is to focus on the key messages conveyed in the paper, and not to provide a complete detailed explanation.

[//]: # search-replace:
[//]: # \cite{chow2014implementing} --- [(Chow et al)](https://www.nature.com/articles/ncomms5015) 
[//]: # \cite{aharonov1997fault} --- [(Aharonov et al)](https://dl.acm.org/doi/abs/10.1137/S0097539799359385)
[//]: # \cite{barends2014superconducting} --- [(Barends et al)](https://www.nature.com/articles/nature13171) 
[//]: # \cite{iontrap_fidelity} --- [(Benhelm et al)](https://www.nature.com/articles/nphys961)

Introduction
======
Quantum algorithms like Shor's factoring, Grover's search and Deutsch-Jozsa algorithms have demonstrated the advantage of quantum computers over classical ones in terms of computational time complexity. However, the presence of noise in quantum circuits limits the types of problems that can be solved using quantum hardware. This gives rise to a fundamental question - is it possible to perform computations using noisy components with an arbitrarily small error? The ability to perform quantum computations with arbitrarily high reliability using noisy components is called fault-tolerant quantum computing (FTQC), which can be achieved by encoding logical qubits over a large number of physical qubits using a suitable quantum error correction (QEC) code. In this context, the threshold theorem of FTQC states that if the fidelity of each component is above a certain threshold, then it is possible to achieve arbitrarily small computational error using a suitable QEC code \cite{aharonov1997fault}. This threshold fidelity depends on the specific QEC code used (among several other factors). Among QEC codes, surface codes have gained immense popularity due to their modest threshold fidelity requirements, and simple planar architecture realizable on the current quantum computers. Specifically, FTQC using surface code has three main requirements: gate fidelities greater than 99%, the ability to establish coupling between adjacent qubits to detect and correct errors, and scalable architecture to accommodate a large number of logical qubits.

Prior to \cite{barends2014superconducting}, no physical realization of a quantum system could meet all the three aforementioned requirements of surface code based FTQC. A 3-qubit transmon based quantum processor was realized in \cite{chow2014implementing}, but the 2-qubit gate fidelity was 96%. Some non-superconducting qubit realizations could achieve fidelities higher than $$99%$$, for example, nuclear magnetic resonance with 99.5% \cite{nmr_fidelity} and ion-traps with $$99.3%$$ fidelities \cite{iontrap_fidelity}, but unfortunately, they are difficult to scale.

The main contributions of \cite{barends2014superconducting} are as follows:
A simple linear array of \tu{nearest-neighbor capacitively coupled} Xmons (cross-shaped transmons) is proposed - since Xmons belong to the family of superconducting qubits, they can be fabricated on a chip making them \tu{scalable}. In this context, scalability implies the ability to accommodate a large number of qubits without too much overhead. Secondly, a novel implementation of 2 qubit gate by fast adiabatic qubit frequency tuning is proposed, which helps in achieving a high fidelity of 99.4% for a two-qubit gate (C-Z gate) - this is greater than the fault-tolerant threshold for surface code protected quantum circuits, and the fidelity of one-qubit gate is improved from 99.7% in prior work \cite{chow2014implementing} to 99.92%, forming a \tu{universal set of gates} ($$R_x(\theta)$$, $$R_y(\theta)$$, and controlled-Z) with \tu{high fidelity}. Therefore, it is a first step towards achieving a fault-tolerant quantum computer.


Circuit architecture
======
[Fig 1. Architecture of an Xmon based circuit](/images/xmon_archietecture.png)

Implementation of high fidelity C-Z gate by fast adiabatic frequency tuning
======
[Fig 2. Energy levels of capacitively coupled nearest neighbor Xmons. a) Energy levels with no detuning, b) Spectrum of joint two-qubit system (uncoupled), and c) Spectrum of joint two-qubit system with capacitive coupling.](/images/energy_levels_adiabatic_cz_4.png)
[Energy levels at every stage of CZ operation and acquisition of phase $$=\pi$$ by the computational state $$\ket{11}$$.](/images/energy_levels_adiabatic_cz_3.png)
[Fast adiabatic trajectory to implement a CZ gate shown by dashed and directed dark blue curve (labeled as $$\ket{1_B 1_A}$$).](/images/adiabatic_trajectory.png)

Results
======


Conclusion
======

