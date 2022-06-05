# Delay-IRB
 `delay` instruction can now be interleaved in the IRB sequence as of my [PR](https://github.com/Qiskit/qiskit-experiments/pull/776).
 
 ### Why Delay
 1. An arbitrary duration(multiple of 16dt) of delay infidelity let us know how well the system keep the qubit state(coherence) especially when there is no operation.
 2. For more than three qubit IRB, we can investigate the infidelity related to the spectator qubit. e.g) Compare the infidelity of three qubit IRB(CX+Delay) with normal simultaneous two qubit IRB(CX) and one qubit IRB(Delay) and see whether 1&2qubit IRB can estimate 3qubit IRB results.
 3. Evaluate how well the theory explain the real world by comparing infidelity of Delay IRB. Figure out if the affect of other factor is large(Theoretical CLE<<Delay IRB) or small(Theoretical CLE~Delay IRB)
 ------
 ### Issues
 1. Expected CLE~Delay IRB<Gate(1q or 2q)error. However, both 1q and 2q showed **CLE<Gate error<Delay** on most backends.![image (1)](https://user-images.githubusercontent.com/56623045/172032331-eabb1dd3-64bc-46d3-a3ec-be42b1b6672c.png) ![image](https://user-images.githubusercontent.com/56623045/172032338-80accdb4-2e0b-4e4e-b84c-81b8af3a9439.png)
 2. The timing of error rate comparision between CLE and Delay IRB incurs different gate calibration and reference sequence -> make a new module `DoubleIRB` which provides common reference RB sequence among all experiments.

