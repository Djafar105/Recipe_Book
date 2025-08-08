# Synaptic Integration
## Jargon
* **EPSP** : Excitatory Post Synaptic Potential 
* **IPSP** : Inhibitory Post Synaptic Potential 
***
## Breakdown 
* First off, we need to clarify the concept of **reversal potential** (previously discussed [[]]). It can be described as the Nernst equilibrium potential for one or multiple ions to which a membrane channel is selective. This **E<sub>rev</sub>** is directly determined by the concentration gradient, the relative fraction of ion concentrations inside and outside the cell [[]]. So, in effect, this potential acts as a **barrier**, a ***seuil***:
	- Relative to the resting membrane potential, **E<sub>rev</sub>** can act as either the **limit of depolarization** (if it's above resting potential) or the **limit of hyperpolarization** (if it's below it).
	- Past this point, no flux is possible in the “normal” way.
- Whether a post-synaptic potential qualifies as an **EPSP** or **IPSP** is heavily dependent on whether the **E<sub>rev</sub>** is above or below the **action potential threshold** at the moment the potential is generated:
	- If **E<sub>rev</sub>** is above threshold, the cell can theoretically reach it —> this is an **EPSP**.
	- If it's below threshold, it acts as a hyperpolarizing force —> an **IPSP**.
* A neurotransmitter can have **excitatory** or **inhibitory** effects — it all depends on the **concentration gradient**, not on the molecule itself.
	==> A strong example is **GABA**: long known to be inhibitory by nature, it can in fact exert excitatory effects in **immature neurons** (as shown in mice, and likely in humans too).
	- Mechanistically, GABA channels are **Cl⁻-selective** : in **mature neurons**, intracellular Cl⁻ is **lower** than outside, due to the presence of an extrusion pump that actively removes Cl⁻. And In **immature neurons**, a different transporter actively **imports** Cl⁻ into the cell, reversing the gradient. As a result, **E<sub>Cl⁻eq</sub>** = **E<sub>rev</sub>** lies **above** the threshold ==>GABA becomes **excitatory**, not inhibitory.
    ![Pasted image 20250808121155.png](Pasted%20image%2020250808121155.png)
***

## Synaptic summation 
* The postsynaptic membrane receives inputs from multiple presynaptic neurons simultaneously. Each input has its own signal intensity and type , either excitatory or inhibitory. These inputs generate synaptic currents that flow into the postsynaptic cell and merge. The result is a hybrid postsynaptic potential, shaped by an algebraic summation of the individual signal amplitudes.
	![synaptic summation.png](synaptic%20summation.png)