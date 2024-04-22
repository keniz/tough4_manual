# EOS3

1. **Description**

This module is an adaptation of the EOS module of the early TOUGH simulator, and implements the same thermophysical properties model (Pruess, 1987). All water properties are represented by the steam table equations as given by the International Formulation Committee (1967). Air is approximated as an ideal gas, and additivity is assumed for air and vapor partial pressures in the gas phase, _Pg = Pa + Pv_. The viscosity of air-vapor mixtures is computed from a formulation given by Hirschfelder et al. (1954). The solubility of air in liquid water is represented by Henry's law, as follows.&#x20;

$$P_a=K_hx^a_{aq}$$                                                                                                                         (7-2)

where $$K_h$$ is Henry’s constant and $$x^a_{aq}$$ is air mole fraction in the aqueous phase. Henry's constant for air dissolution in water is a slowly varying function of temperature, varying from $$6.7 \times 10^9$$Pa at 20 ˚C to $$1.0\times10^{10}$$ Pa at 60 ˚C and $$1.1 \times 10^{10}$$ Pa at 100 ˚C (Loomis, 1928). Because air solubility is small, this kind of variation is not expected to cause significant effects, and a constant $$K_h=10^{10}$$ Pa was adopted.

2. **Specifications**

A summary of EOS3 specifications and parameters is given in Table 7. The default number of mass components is 2. Simulation can be run in isothermal or non-isothermal. The default choice of primary thermodynamic variables is (P, Xair, T) for single-phase, (Pg, Sg + 10, T) for two-phase conditions, which remains the same as used in TOUGH3/EOS3. The reason using Sg+10 as primary variable is for distinguishing the phase condition based on value range of the second primary variable.  For this reason, input of phase state name as part of the initial conditions is not necessary for EOS3. The last primary variable is always temperature no matter if the simulation is in isothermal or non-isothermal, but in isothermal simulation the energy equation does not need to be solved and temperature is always constant.&#x20;

Different to TOUGH3, TOUGH4 does not require the input of (NK, NEQ, NPH, NB) to define the flow system. These parameters are determined internally by user selection of the mass components and other options. EOS3 in TOUGH4 allows turning on vapor pressure lowering simulation which is not available in TOUGH3.&#x20;

Table 7 Summary for EOS3

<table><thead><tr><th width="282">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) AIR</p><p>(3-7) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) two-phase, AQG</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eos3.md">Table 21</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Vapor pressure Lowering, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation. </td></tr></tbody></table>

