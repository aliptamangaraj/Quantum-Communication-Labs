```
import numpy as np
from qiskit import QuantumCircuit
from qiskit.quantum_info import Kraus, SuperOp, Statevector, DensityMatrix, partial_trace, state_fidelity
from qiskit.visualization import plot_histogram
from qiskit.transpiler import generate_preset_pass_manager
from qiskit_aer import AerSimulator
from qiskit_aer.noise import (
NoiseModel,
QuantumError,
ReadoutError,
depolarizing_error,
pauli_error,
thermal_relaxation_error,
)
alpha = np.sqrt(0.3)
beta = np.sqrt(0.7)
psi = Statevector([alpha, beta])
print(psi)
qc = QuantumCircuit(3,2)
qc.initialize(psi.data,0)
qc.h(1)
qc.cx(1,2)
qc.cx(0,1)
qc.h(0)
qc.measure(0, 0)
qc.measure(1, 1)
with qc.if_test((1, 1)):
qc.x(2)
with qc.if_test((0, 1)):
qc.z(2)
qc.barrier()
qc.measure_all()
qc.draw()

p_error = 0.05
bit_flip = pauli_error([("X", p_error), ("I", 1 - p_error)])
phase_flip = pauli_error([("Z", p_error), ("I", 1 - p_error)])
print(bit_flip)
print(phase_flip)
bitphase_flip = bit_flip.compose(phase_flip)
print(bitphase_flip)
error2 = phase_flip.tensor(bit_flip)
print(error2)
bit_flip_kraus = Kraus(bit_flip)
print(bit_flip_kraus)
phase_flip_sop = SuperOp(phase_flip)
print(phase_flip_sop)
print(QuantumError(bit_flip_kraus))
QuantumError(bit_flip_kraus) == bit_flip
p0given1 = 0.1
p1given0 = 0.05
ReadoutError([[1 - p1given0, p1given0], [p0given1, 1 - p0given1]])
#All-qubit quantum error
noise_model = NoiseModel()
error1 = depolarizing_error(0.05, 1)
noise_model.add_all_qubit_quantum_error(error1, ["h", "x", "z"])
error2 = depolarizing_error(0.05, 2)
noise_model.add_all_qubit_quantum_error(error2, ["cx"])
print(noise_model)
sim_ideal = AerSimulator(noise_model=noise_model)
result_ideal = sim_ideal.run(qc).result()
plot_histogram(result_ideal.get_counts(0))
import matplotlib.pyplot as plt
plt.show()
```
