
# Quantum Circuit & Entanglement Sandbox

**Live Deployment:** [https://optimus-coders.web.app/](https://optimus-coders.web.app/)  
**Platform Architecture:** React 19 · TypeScript · Three.js (WebGL) · React Flow · Vite · Tailwind CSS · Firebase Hosting

---

## 1. Executive Abstract

The **Quantum Circuit & Entanglement Sandbox** is an interactive, browser-based quantum computing laboratory and simulation platform designed for students, researchers, and quantum software engineers. It bridges the gap between abstract quantum mathematical formalism and intuitive physical visualization by providing a real-time, zero-latency execution engine for 1-qubit and 2-qubit quantum circuits.

Users can assemble quantum circuits using a dual-paradigm editor (traditional quantum wire rails or node-based Directed Acyclic Graph via React Flow), step through state evolutions with continuous unitary interpolation, inspect 3D Bloch sphere vector rotations, perform multi-shot Monte Carlo measurements across arbitrary bases, analyze reduced density matrices and entanglement concurrence, export code directly to **OpenQASM** and **IBM Qiskit**, and hone their intuition through a gamified CTF (Capture The Flag) challenge mode.

---

## 2. Comprehensive Feature Breakdown

### A. Real-Time 3D Bloch Sphere Visualizer (Three.js / WebGL)
* **Full 3D State Vector Rendering:** Projects single-qubit pure and mixed states onto a celestial sphere with orbit controls, pan, zoom, and auto-rotation.
* **Direct Surface Interaction & Raycasting:** Enables users to grab the state vector with their mouse and drag it along the sphere's surface, dynamically reverse-calculating the corresponding $(\theta, \phi)$ spherical angles and synthesizing required rotation gates.
* **Unitary Trajectory Arcs (SLERP):** Visualizes the exact geometric rotation trajectory on the unit sphere during gate transitions using Spherical Linear Interpolation around the gate's rotation axis.
* **Projection & Probability Envelopes:** Renders projection lines down to the $Z$-axis (computational basis probabilities) and equatorial plane ($X-Y$ relative phase).
* **Mixed-State Radius Shrinkage:** When a qubit is entangled in a 2-qubit system, its reduced density matrix becomes mixed; the 3D Bloch vector visually contracts inward from the unit sphere surface toward the origin ($r < 1$).

### B. Dual-Paradigm Circuit Builder & Step-by-Step Debugger
* **Dual View Canvas:**
  * **Flow Mode:** Interactive node-based graph powered by React Flow with drag-and-drop gates, wiring, and custom gate cards.
  * **Wire Mode:** Classic multi-wire quantum score representation familiar from IBM Quantum Composer.
* **Execution & Playback Engine:** Play/pause auto-stepping, single-step forward/backward scrubbing, and variable playback speeds (250ms – 2000ms).
* **Comprehensive Quantum Gate Library:**
  * *Pauli Family:* Identity ($I$), Bit-Flip ($X$), Bit-and-Phase-Flip ($Y$), Phase-Flip ($Z$), and $\sqrt{X}$ ($SX$).
  * *Superposition & Phase:* Hadamard ($H$), Phase ($S, S^\dagger$), $T$-gate ($T, T^\dagger$), arbitrary Phase Shift $P(\phi)$.
  * *Parametric Rotations:* $R_x(\theta)$, $R_y(\theta)$, $R_z(\theta)$ with interactive angle sliders.
  * *Two-Qubit Controlled Gates:* Controlled-NOT ($CX$), Controlled-$Z$ ($CZ$), and $SWAP$.
  * *Measurement & State Prep:* Projective measurement ($M_z, M_x$) and unconditional ground-state reset ($|0\rangle$).
* **Preset Circuit Library:** Instant loading of standard quantum workflows including Bell States ($|\Phi^+\rangle, |\Psi^-\rangle$), Superdense Coding, Quantum Coin Flipping, Phase Flip (H-Z-H), and Swap tests.
* **Industry Code Export:** Real-time generation of executable **OpenQASM 2.0 / 3.0** scripts and Python **IBM Qiskit** code snippets with one-click clipboard copying.

### C. 1,000-Shot Monte Carlo Measurement Simulator
* **Stochastic Wavefunction Collapse:** Simulates physical quantum hardware measurements subject to Born's Rule.
* **Configurable Measurement Bases:** Run simulations in the $Z$-basis ($\{|0\rangle, |1\rangle\}$), $X$-basis ($\{|+\rangle, |-\rangle\}$), or $Y$-basis ($\{|i\rangle, |-i\rangle\}$).
* **Statistical Comparison:** Side-by-side empirical histograms against exact theoretical probabilities with cumulative error metrics.
* **Single-Shot Audit Trail:** Step-by-step collapse log recording discrete experimental trials.

### D. Mathematical Inspector & Formalism Analyzer
* **Dirac Ket State Vector:** Exact expansion in the computational basis ($\mathbb{C}^2$ or $\mathbb{C}^4$) with formatted complex amplitudes:
  $$\alpha = a + bi, \quad \beta = c + di$$
* **Density Matrix Display ($\rho$):** Real-time matrix representation displaying diagonal populations and off-diagonal coherences.
* **Step-by-Step Unitary Transformation Matrix:** Explicit 2D matrix multiplication breakdown:
  $$U |\psi_{\text{in}}\rangle = |\psi_{\text{out}}\rangle$$
* **Entanglement Metrics:** Live calculation of Wootters Concurrence $C$, state purity $\text{Tr}(\rho^2)$, and separable vs. entangled classification.

### E. Gamified CTF (Capture the Flag) Challenge Mode
An interactive series of cryptanalysis and quantum-state engineering challenges:
1. **SEC-01 (Operation Superposition):** Synthesize the $|+\rangle$ state from ground $|0\rangle$.
2. **SEC-02 (Equatorial Phase Decryption):** Perform a $+90^\circ$ Z-axis equatorial rotation to reach $|i\rangle$.
3. **SEC-03 (Pauli-X Bypass Protocol):** Invert $|0\rangle \to |1\rangle$ without using the hardware $X$ gate ($H \to Z \to H$ or $R_y(\pi)$).
4. **SEC-04 (Bell State Entanglement Link):** Establish maximally entangled EPR channel $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$.
5. **SEC-05 (The Anti-Correlated Singlet):** Construct the antisymmetric singlet state $|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$.
6. **SEC-06 (Quantum Teleportation Kernel):** Reverse-engineer superdense encoding/decoding circuit achieving 100% deterministic fidelity on target bitstring $|11\rangle$.
* *Includes hints, live automated state validation against tolerance thresholds, persistent progress tracking (LocalStorage), flag reveals, and confetti animations.*

---

## 3. Quantum Computing Theory & Mathematical Foundations

### 1. State Vectors & The Hilbert Space
In quantum mechanics, a single qubit exists as a normalized vector in a two-dimensional complex Hilbert space $\mathcal{H}_2 \cong \mathbb{C}^2$, spanned by the orthonormal computational basis states:
$$|0\rangle = \begin{bmatrix} 1 \\ 0 \end{bmatrix}, \quad |1\rangle = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

An arbitrary pure state $|\psi\rangle$ is a linear superposition:
$$|\psi\rangle = \alpha |0\rangle + \beta |1\rangle, \quad \alpha, \beta \in \mathbb{C}$$

subject to the Born normalization condition:
$$\langle \psi | \psi \rangle = |\alpha|^2 + |\beta|^2 = 1$$

---

### 2. The Bloch Sphere Representation
Factoring out an unobservable global phase $e^{i\gamma}$, any single-qubit pure state can be uniquely parameterized by two real angles $\theta \in [0, \pi]$ (polar angle) and $\phi \in [0, 2\pi)$ (azimuthal phase):
$$|\psi\rangle = \cos\left(\frac{\theta}{2}\right) |0\rangle + e^{i\phi}\sin\left(\frac{\theta}{2}\right) |1\rangle$$

This state maps to a unit vector $\vec{r} = (x, y, z)$ on the surface of the **Bloch Sphere**:
$$x = \sin\theta \cos\phi = 2\,\text{Re}(\alpha^* \beta)$$
$$y = \sin\theta \sin\phi = 2\,\text{Im}(\alpha^* \beta)$$
$$z = \cos\theta = |\alpha|^2 - |\beta|^2 = P(|0\rangle) - P(|1\rangle)$$

Key landmarks on the sphere:
* **North Pole $(z = +1)$:** Ground state $|0\rangle$ ($\theta = 0$)
* **South Pole $(z = -1)$:** Excited state $|1\rangle$ ($\theta = \pi$)
* **Equator $(z = 0)$:** Equal superposition states:
  * $+X$ axis: $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
  * $-X$ axis: $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$
  * $+Y$ axis: $|i\rangle = \frac{1}{\sqrt{2}}(|0\rangle + i|1\rangle)$
  * $-Y$ axis: $|-i\rangle = \frac{1}{\sqrt{2}}(|0\rangle - i|1\rangle)$

---

### 3. Unitary Transformations (Quantum Gates)
All reversible quantum operations are represented by unitary operators $U \in U(2^n)$ satisfying:
$$U^\dagger U = U U^\dagger = I$$

This ensures inner-product preservation and probability conservation.

#### Pauli Matrices
$$\sigma_x = X = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}, \quad \sigma_y = Y = \begin{bmatrix} 0 & -i \\ i & 0 \end{bmatrix}, \quad \sigma_z = Z = \begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix}$$

#### Superposition and Phase Gates
* **Hadamard Gate:** Creates equal superposition from basis states:
  $$H = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}, \quad H|0\rangle = |+\rangle, \quad H|1\rangle = |-\rangle$$
* **Phase Gate ($S$):** Applies a $\frac{\pi}{2}$ phase rotation ($S = \sqrt{Z}$):
  $$S = \begin{bmatrix} 1 & 0 \\ 0 & i \end{bmatrix}$$
* **$T$ Gate ($\pi/8$):** Non-Clifford gate essential for universal quantum computation:
  $$T = \begin{bmatrix} 1 & 0 \\ 0 & e^{i\pi/4} \end{bmatrix}$$

#### Parametric Rotation Operators
Rotations by an angle $\theta$ about the $\hat{n} = (n_x, n_y, n_z)$ axis:
$$R_{\hat{n}}(\theta) = \exp\left(-i\frac{\theta}{2} (\hat{n} \cdot \vec{\sigma})\right) = \cos\left(\frac{\theta}{2}\right)I - i\sin\left(\frac{\theta}{2}\right)(\hat{n} \cdot \vec{\sigma})$$

* **$R_x(\theta)$:** $\begin{bmatrix} \cos(\theta/2) & -i\sin(\theta/2) \\ -i\sin(\theta/2) & \cos(\theta/2) \end{bmatrix}$
* **$R_y(\theta)$:** $\begin{bmatrix} \cos(\theta/2) & -\sin(\theta/2) \\ \sin(\theta/2) & \cos(\theta/2) \end{bmatrix}$
* **$R_z(\theta)$:** $\begin{bmatrix} e^{-i\theta/2} & 0 \\ 0 & e^{i\theta/2} \end{bmatrix}$

---

### 4. Two-Qubit States & Quantum Entanglement
A composite two-qubit system lives in the tensor product space $\mathcal{H}_4 = \mathcal{H}_2 \otimes \mathcal{H}_2 \cong \mathbb{C}^4$:
$$|\Psi\rangle = c_{00}|00\rangle + c_{01}|01\rangle + c_{10}|10\rangle + c_{11}|11\rangle$$

where $\sum_{i,j} |c_{ij}|^2 = 1$.

#### Separability vs. Entanglement
* A state is **separable** (product state) if it can be factored into $|\psi_1\rangle \otimes |\psi_2\rangle$.
* A state is **entangled** if no such factorization exists. Measuring one qubit instantaneously determines the state of the other, regardless of spatial separation (Einstein's "spooky action at a distance").

#### The 4 Bell States (EPR Pairs)
Maximally entangled orthonormal basis states:
$$|\Phi^+\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}, \quad |\Phi^-\rangle = \frac{|00\rangle - |11\rangle}{\sqrt{2}}$$
$$|\Psi^+\rangle = \frac{|01\rangle + |10\rangle}{\sqrt{2}}, \quad |\Psi^-\rangle = \frac{|01\rangle - |10\rangle}{\sqrt{2}}$$

#### Two-Qubit Controlled Gates
* **Controlled-NOT (CNOT / $CX$):** Flips target qubit $q_1$ if control qubit $q_0 = |1\rangle$:
  $$\text{CNOT} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{bmatrix}$$
* Creating a Bell state:
  $$|00\rangle \xrightarrow{H \otimes I} \frac{|0\rangle + |1\rangle}{\sqrt{2}} \otimes |0\rangle = \frac{|00\rangle + |10\rangle}{\sqrt{2}} \xrightarrow{\text{CNOT}} \frac{|00\rangle + |11\rangle}{\sqrt{2}} = |\Phi^+\rangle$$

---

### 5. Density Matrices, Partial Trace, and Mixed States
For a composite state $\rho_{AB} = |\Psi\rangle\langle\Psi|$, the local subsystem of qubit $A$ is obtained via the **Partial Trace** over subsystem $B$:
$$\rho_A = \text{Tr}_B(\rho_{AB}) = \sum_{k \in \{0, 1\}} (I \otimes \langle k|) \rho_{AB} (I \otimes |k|)$$

For a maximally entangled Bell state $|\Phi^+\rangle$:
$$\rho_A = \text{Tr}_B\left(\frac{|00\rangle + |11\rangle}{\sqrt{2}}\frac{\langle 00| + \langle 11|}{\sqrt{2}}\right) = \frac{1}{2}\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = \frac{I}{2}$$

* The reduced state has **zero purity** ($\gamma = \text{Tr}(\rho^2) = \frac{1}{2}$, maximally mixed).
* Its Bloch vector length is $r = \|\vec{r}\| = 0$, sitting precisely at the center of the sphere.

#### Wootters Concurrence
For a pure two-qubit state $|\Psi\rangle = c_{00}|00\rangle + c_{01}|01\rangle + c_{10}|10\rangle + c_{11}|11\rangle$, entanglement is quantified by the **Concurrence** $C \in [0, 1]$:
$$C(|\Psi\rangle) = 2\,|c_{00}c_{11} - c_{01}c_{10}|$$

* $C = 0 \implies$ Product / separable state.
* $C = 1 \implies$ Maximally entangled state (e.g., Bell states).

---

### 6. Quantum Measurement & Born's Rule
According to the measurement postulate, an observable $M = \sum_m m P_m$ collapses state $|\psi\rangle$ into eigenstate $|m\rangle$ with probability:
$$P(m) = \langle\psi| P_m |\psi\rangle = \text{Tr}(P_m \rho)$$

In the computational $Z$-basis:
$$P(0) = |\langle 0|\psi\rangle|^2 = |\alpha|^2, \quad P(1) = |\langle 1|\psi\rangle|^2 = |\beta|^2$$

Post-measurement, the statevector undergoes projection:
$$|\psi'\rangle = \frac{P_m |\psi\rangle}{\sqrt{P(m)}}$$

---

## 4. Summary Table of Core Specifications

| Dimension | Specification |
| :--- | :--- |
| **Qubit Capacity** | 1-Qubit & 2-Qubit interactive state space ($\mathbb{C}^2 \to \mathbb{C}^4$) |
| **3D Engine** | Three.js WebGL with anti-aliasing, PBR lighting, arc SLERP trajectories, and raycast interaction |
| **Circuit Editor** | React Flow dynamic DAG & custom multi-wire quantum grid rails |
| **Supported Gates** | $I, X, Y, Z, SX, H, S, S^\dagger, T, T^\dagger, R_x(\theta), R_y(\theta), R_z(\theta), P(\phi), CX, CZ, SWAP, M_z, M_x, \text{Reset}$ |
| **Simulation Methods** | Exact Statevector ($\mathbb{C}^n$), Density Matrix ($\rho$), and 1,000-shot Monte Carlo simulation |
| **Entanglement Metrics**| Wootters Concurrence ($C$), Reduced Density Matrix ($\text{Tr}_B$), Purity ($\text{Tr}(\rho^2)$) |
| **Export Formats** | OpenQASM 2.0 / 3.0, Python IBM Qiskit |
| **CTF Challenges** | 6 gamified scenarios covering Superposition, Phase, Gates, Entanglement, and Teleportation |
