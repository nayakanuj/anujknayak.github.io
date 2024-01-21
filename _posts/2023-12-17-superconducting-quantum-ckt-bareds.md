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
[//]: # [(Chow et al)](https://www.nature.com/articles/ncomms5015) --- [(Chow et al)](https://www.nature.com/articles/ncomms5015) 
[//]: # [(Aharonov et al)](https://dl.acm.org/doi/abs/10.1137/S0097539799359385) --- [(Aharonov et al)](https://dl.acm.org/doi/abs/10.1137/S0097539799359385)
[//]: # [(Barends et al)](https://www.nature.com/articles/nature13171) --- [(Barends et al)](https://www.nature.com/articles/nature13171) 
[//]: # [(Benhelm et al)](https://www.nature.com/articles/nphys961) --- [(Benhelm et al)](https://www.nature.com/articles/nphys961)

Introduction
======
Quantum algorithms like Shor's factoring, Grover's search and Deutsch-Jozsa algorithms have demonstrated the advantage of quantum computers over classical ones in terms of computational time complexity. However, the presence of noise in quantum circuits limits the types of problems that can be solved using quantum hardware. This gives rise to a fundamental question - is it possible to perform computations using noisy components with an arbitrarily small error? The ability to perform quantum computations with arbitrarily high reliability using noisy components is called fault-tolerant quantum computing (FTQC), which can be achieved by encoding logical qubits over a large number of physical qubits using a suitable quantum error correction (QEC) code. In this context, the threshold theorem of FTQC states that if the fidelity of each component is above a certain threshold, then it is possible to achieve arbitrarily small computational error using a suitable QEC code [(Aharonov et al)](https://dl.acm.org/doi/abs/10.1137/S0097539799359385). This threshold fidelity depends on the specific QEC code used (among several other factors). Among QEC codes, surface codes have gained immense popularity due to their modest threshold fidelity requirements, and simple planar architecture realizable on the current quantum computers. Specifically, FTQC using surface code has three main requirements: gate fidelities greater than 99%, the ability to establish coupling between adjacent qubits to detect and correct errors, and scalable architecture to accommodate a large number of logical qubits.

Prior to [(Barends et al)](https://www.nature.com/articles/nature13171), no physical realization of a quantum system could meet all the three aforementioned requirements of surface code based FTQC. A 3-qubit transmon based quantum processor was realized in [(Chow et al)](https://www.nature.com/articles/ncomms5015), but the 2-qubit gate fidelity was 96%. Some non-superconducting qubit realizations could achieve fidelities higher than 99%, for example, nuclear magnetic resonance with 99.5% [(Ryan et al)](https://iopscience.iop.org/article/10.1088/1367-2630/11/1/013034/meta) and ion-traps with 99.3% fidelities [(Benhelm et al)](https://www.nature.com/articles/nphys961), but unfortunately, they are difficult to scale.

The main contributions of [(Barends et al)](https://www.nature.com/articles/nature13171) are as follows:
A simple linear array of \tu{nearest-neighbor capacitively coupled} Xmons (cross-shaped transmons) is proposed - since Xmons belong to the family of superconducting qubits, they can be fabricated on a chip making them \tu{scalable}. In this context, scalability implies the ability to accommodate a large number of qubits without too much overhead. Secondly, a novel implementation of 2 qubit gate by fast adiabatic qubit frequency tuning is proposed, which helps in achieving a high fidelity of 99.4% for a two-qubit gate (C-Z gate) - this is greater than the fault-tolerant threshold for surface code protected quantum circuits, and the fidelity of one-qubit gate is improved from 99.7% in prior work [(Chow et al)](https://www.nature.com/articles/ncomms5015) to 99.92%, forming a \tu{universal set of gates} ($$R_x(\theta)$$, $$R_y(\theta)$$, and controlled-Z) with \tu{high fidelity}. Therefore, it is a first step towards achieving a fault-tolerant quantum computer.


Circuit architecture
======
![](/personal_webpage/images/xmon_architecture.png)
*Fig 1. Architecture of an Xmon based circuit*

Implementation of high fidelity C-Z gate by fast adiabatic frequency tuning
======

The novelty of the paper [(Barends et al)](https://www.nature.com/articles/nature13171) is the realization of a high-fidelity controlled-Z gate by fast adiabatic tuning, which is explained in this section. First, let us describe the spectrum of a joint system of two Xmons. Suppose the energy levels of a joint system of two Xmon qubits A and B with different excitation frequencies are as shown in Figure 2. Let $$\alpha$$ denote the detuning of qubit A with respect to qubit B. When the qubits are not coupled, the energy levels $$\ket{20}$$ and $$\ket{11}$$ cross over at a specific detuning frequency. Thanks to anharmonicity and different excitation frequencies of the two qubits, the detuning frequencies corresponding to the cross-over points are different for the pair $$\ket{20}$$, $$\ket{11}$$ and the pair $$\ket{10}$$, $$\ket{01}$$. However, if the qubits are coupled, then they hybridize and the energy levels don’t cross as shown Figure 2(c).

For a quantum system at the $$n^{th}$$ eigenstate, the adiabatic evolution of the Hamiltonian results in the system maintaining its presence in the $$n^{th}$$ eigenstate, concurrently acquiring a phase factor (called as Berry phase). Suppose the initial state of the qubit pair is $$\ket{11}$$, then applying a flux bias current results in a constant flux, which detunes qubit A relative to qubit B such that $$\ket{20}$$ is aligned with $$\ket{11}$$. Since the qubits are coupled, the qubits perform Rabi oscillations between $$\ket{11}$$ and $$\ket{20}$$, while acquiring a phase of $$i$$ in every transition (half oscillation). The oscillation frequency is equal to the difference in the hybridized energy levels, which is proportional to the coupling constant $$g$$ between the two qubits. Now, if we wait for a fixed duration of time (around $$43$$ ns, which includes the Gaussian phase for switching on, flat duration, and the Gaussian switch off phase), the state $$\ket{11}$$ acquires a negative phase. Now, turning off flux bias current reverts the qubit A back to the original detuning. At the end of this adiabatic trajectory, the state $$\ket{11}$$ will have acquired a negative phase (Please refer to Figure 3 for illustration).


This happens only for state $$\ket{11}$$ and all other states remain unchanged since they do not interact with any other energy levels – in other words, this is an implementation of a controlled Z operation. The entire gate operation completes in 43 ns, which is a significant improvement over its transmon predecessor which took about 350 ns \cite{barends2013coherent} for a two-qubit gate operation. The improvement in gate operation time is due to direct capacitive coupling between the neighboring qubits (with a large coupling frequency of $$g/2\pi = 30$$ MHz) instead of each qubit capacitively coupling to a common bus resonator. This additional degree of separation between qubits in [(Chow et al)](https://www.nature.com/articles/ncomms5015) resulted in a smaller coupling constant. In [(Barends et al)](https://www.nature.com/articles/nature13171), a faster gate means that there is less room for dephasing, which is one of the primary reasons for the high fidelity of this realization of the CZ gate.

One may ask, can we make this operation even faster? - attempting this would lead to the following issues: the detuning trajectory may not be adiabatic, which could worsen the leakage to a non-computational state $$\ket{20}$$. Upon reaching the avoided crossing, the controlled-Z gate duration is also limited by the coupling constant between the qubits (gate duration is inversely proportional to $$g$$). Therefore, to achieve high fidelity of a two-qubit gate, we need to operate fast enough to not let the quantum state decohere, and at the same time slow enough to maintain adiabaticity (minimize the leakage to non-computational state). This can be achieved by optimizing the detuning, phase accumulation and reverting trajectory as shown in Figure 4.

![](/personal_webpage/images/energy_levels_adiabatic_cz_4.png)
*Fig 2. Energy levels of capacitively coupled nearest neighbor Xmons. a) Energy levels with no detuning, b) Spectrum of joint two-qubit system (uncoupled), and c) Spectrum of joint two-qubit system with capacitive coupling.*
![](/personal_webpage/images/energy_levels_adiabatic_cz_3.png)
*Energy levels at every stage of CZ operation and acquisition of phase $$=\pi$$ by the computational state $$\ket{11}$$.*
![](/personal_webpage/images/adiabatic_trajectory.png)
*Fast adiabatic trajectory to implement a CZ gate shown by dashed and directed dark blue curve (labeled as $$\ket{1_B 1_A}$$).*

Results
======

A straightforward way to evaluate the gate fidelity is to arbitrarily initialize the qubits and perform gate operation under evaluation followed by measurement. However, this procedure does not provide true fidelity of the gate since it does not consider the errors in state preparation and measurement. Therefore, we need a way to isolate the fidelity of the gate from other sources of error.

Benchmarking of the fidelity of gates is performed in the following manner: first, consider a reference circuit that performs random Clifford gates $m$ times followed by a recovery gate that undoes all the previous $m$ gates resulting in an overall identity operation (supposing the gates are noiseless). The fidelity of this sequence of gates forms a reference that captures the initialization and measurement errors. Secondly, the gate under evaluation, is interleaved with the same set of random Clifford gates $m$ times, and a final recovery gate (different from the reference circuit) is appended at the end of the chain of gates such that the entire operation is equivalent to identity. Now, the gate fidelity can be inferred from the difference in fidelities between the reference circuit and interleaved circuit. In Figure 5, x-axis is the depth of the circuit, y-axis is the sequence fidelity. Black solid curve corresponds to 100\% fidelity and the dashed curve to 99\% fidelity. The two-qubit CZ gate has a fidelity$>$99\% at all depths.

![](personal_webpage/images/CZ_benchmarking1.png)
*Sequence fidelity vs circuit depth ($$m$$). The sequence fidelity of CZ gate is sandwiched between the sequence fidelity of reference circuit (black solid curve) and sequence fidelity of 99% (black dashed curve). Therefore, CZ has a circuit fidelity of $$>99%$$.*

Conclusion
======
In this blogpost, we reviewed an Xmon-based superconducting quantum circuit, which demonstrated high gate fidelities for a universal set of quantum gates. We also discussed the process of fast adiabatic qubit frequency detuning to implement a CZ gate, which resulted in improving the state-of-the-art two-qubit gate fidelity to 99.4\%. Consequently, a universal set of gates could be synthesized that exceeded the threshold fidelity required by the surface code. The simple and modular Xmon architecture helped in creating a linear array of qubits, which is potentially scalable beyond 5 qubits. This work brought us a step closer to the goal of achieving a fully fault-tolerant quantum computation. 

Some open questions not addressed by this work are as follows: First, to implement surface code, a linear array is not sufficient - a 2D array of data qubits and ancillas in a checkerboard pattern is required. The authors of paper [(Barends et al)](https://www.nature.com/articles/nature13171) propose a 2D architecture (in supplementary material), but without performance analysis. Therefore, practical extension of the current Xmon architecture is still an open (most likely engineering) challenge (at the time of publication of [(Barends et al)](https://www.nature.com/articles/nature13171)).
Second, to perform meaningful quantum computations we need long-range coupling between logical qubits (formed by patches of several physical qubits) - the routing between logical qubits is not addressed in the paper, which makes realizing a truly fault-tolerant quantum computer still a work in progress.
