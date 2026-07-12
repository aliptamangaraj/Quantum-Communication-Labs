# Objectives

1. Create an entangled Bell pair.
2. Perform Bell-state measurement.
3. Apply classical feed-forward corrections.
4. Simulate teleportation of the default state ∣0⟩.
5. Visualize the quantum circuit.

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

| Qubit | Purpose |
| q0 | Alice's entangled qubit |
| q1 | Bob's entangled qubit |
| q2 | Information qubit |

---

## Initial State

The information qubit is prepared as:

∣ψ⟩=α∣0⟩+β∣1⟩

For simplicity:

∣ψ⟩=(∣0⟩+∣1⟩)/√2

---

## Bell Pair Generation

Create entanglement between q0 and q1.

Apply:

1. Hadamard gate
2. CNOT gate

Result:

∣Φ+⟩=(∣00⟩+∣11⟩)/√2

# Teleportation Protocol

### Step 1

Entangle the information qubit with Alice's qubit.

Apply:

- CNOT(q0,q2)

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
    01             X 
    10             Z
    11            XZ 

---

### Step 6

Bob's qubit now becomes:

∣ψ⟩

which is the original quantum state.
