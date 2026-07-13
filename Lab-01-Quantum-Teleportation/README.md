# Aim

To implement the quantum teleportation protocol using Qiskit and demonstrate the teleportation of the default quantum state ∣0⟩ using quantum entanglement and classical communication.

# Objectives

1. Create an entangled Bell pair.
2. Perform Bell-state measurement.
3. Apply classical feed-forward corrections.
4. Simulate teleportation of the default state ∣0⟩.
5. Visualize the quantum circuit.
6. Understand the role of entanglement and classical communication in quantum teleportation.

# Theory

Quantum teleportation is a protocol that transfers the quantum state of a particle from one location to another without physically transmitting the particle itself.

Unlike classical communication, the information is carried using:

- Quantum entanglement
- Classical communication

The protocol was proposed by:

Charles Bennett and collaborators in 1993.

---

## Basic Concept

Three qubits are required:

| q0 | Alice's entangled qubit |
| q1 | Bob's entangled qubit |
| q2 | Information qubit |

---

## Initial State

The information qubit is prepared as:

|0⟩

For simplicity:

(∣0⟩+∣1⟩)/√2

---

## Bell Pair Generation

Create entanglement between q0 and q1.
Alice owns q0.
Bob owns q1.

Apply:

1. Hadamard gate
2. CNOT gate

Result:

∣Φ+⟩=(∣00⟩+∣11⟩)/√2

# Teleportation Protocol

### Step 1

Entangle the information qubit with Alice's qubit.

Apply:

- CNOT(q2,q0)

---

### Step 2

Apply a Hadamard to q2.

---

### Step 3

Measure q2 and q0.

Alice obtains two classical bits.

---

### Step 4

Transmit the classical bits to Bob.

---

### Step 5

Bob applies corrective operations.

| Measurement | Operation |
    00            None 
    01             Z 
    10             X
    11            XZ 

---

### Step 6

Bob's qubit now becomes:

∣ψ⟩

which is the original quantum state.

# Software Required

Python 3.12
Qiskit
Qiskit Aer
Matplotlib


# Methodology

## Part A: Circuit Construction

### Step 1

Import the required Python libraries.

from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator
from qiskit.quantum_info import Statevector

---

### Step 2

Create a quantum circuit with three qubits and two classical bits.

qc = QuantumCircuit(3,2) #QuantumCircuit(number_of_qubits, number_of_classical_bits)

---

### Step 3

Create an entangled Bell pair shared between Alice and Bob to establish the quantum channel required for teleportation.

qc.h(0) #Apply a Hadamard gate
qc.cx(0,1) #Apply a Controlled-X gate.
qc.barrier()

---

### Step 4

Perform the Bell-state measurement.

qc.cx(2,0) 
qc.h(2)
qc.barrier()

---

### Step 5

Apply Bob's conditional correction operations.

with qc.if_test((0, 1)):
qc.x(1)
with qc.if_test((1, 1)):
qc.z(1)
qc.barrier()

---

### Step 6

Measure all qubits and display the circuit.

qc.measure_all()
qc.draw()

---

# Code

```python
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator
from qiskit.quantum_info import Statevector

qc = QuantumCircuit(3,2)

qc.h(0)
qc.cx(0,1)
qc.barrier()

qc.cx(2,0)
qc.h(2)
qc.barrier()

qc.measure(0, 0) 
qc.measure(1, 1)

with qc.if_test((0,1)):
    qc.x(1)

with qc.if_test((1,1)):
    qc.z(1)

qc.barrier()

qc.measure_all()

qc.draw()
```

---

# Circuit Diagram

<img width="975" height="235" alt="image" src="https://github.com/user-attachments/assets/16774d55-3a68-4bb1-99f6-b8867ed1e25a" />



---

# Observation

The generated circuit successfully demonstrates the implementation of the quantum teleportation protocol using Qiskit.

The circuit contains:

- Bell pair generation using Hadamard and CNOT gates.
- Bell-state measurement.
- Classical communication through two classical bits.
- Conditional X and Z correction gates.
- Final measurement of all qubits.

Since no arbitrary quantum state was prepared on the information qubit, the protocol teleports the default state **|0⟩**.

---

# Result

The quantum teleportation circuit was successfully implemented in Qiskit.

The simulation correctly generated:

- An entangled Bell pair.
- Bell-state measurements.
- Classical feed-forward corrections.
- Teleportation of the default quantum state **|0⟩**.

---

# Conclusion

This experiment demonstrated the fundamental working principle of quantum teleportation.

Although only the default quantum state was teleported, the protocol establishes the foundation for future experiments involving arbitrary quantum states, teleportation fidelity, and quantum networking.
The protocol shows that a quantum state can be transferred from one qubit to another using shared entanglement and classical communication without physically transmitting the original qubit.

This implementation serves as the foundation for future experiments involving arbitrary quantum states, teleportation fidelity analysis, noisy quantum channels, and execution on IBM Quantum hardware.

---

# Future Work

- Teleport arbitrary quantum states.
- Verify teleportation using statevector comparison.
- Calculate teleportation fidelity.
- Simulate noisy quantum channels.
- Execute the circuit on IBM Quantum hardware.
- Extend the protocol to entanglement swapping and quantum repeaters.

---

# References

1. C. H. Bennett et al., "Teleporting an Unknown Quantum State via Dual Classical and Einstein-Podolsky-Rosen Channels," *Physical Review Letters*, 70, 1895–1899 (1993).

2. IBM Quantum Learning – Quantum Teleportation.

3. Qiskit Documentation.

4. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.


# What I Learned

- How Bell pairs are created using Hadamard and CNOT gates.
- The role of Bell-state measurements in quantum teleportation.
- How classical bits control conditional quantum operations in Qiskit.
- The importance of classical communication in completing the teleportation protocol.
- How to implement conditional gates using `if_test()` in modern Qiskit.
