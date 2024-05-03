# TMVOC

1. **Description**

TMVOC was originally developed by Karsten Pruess and Alfredo Battistelli. It was designed for simulating the flow of multicomponent mixtures of volatile organic chemicals (VOCs), such as crude oil, gasoline or diesel, and organic solvents, in variably saturated media. It can be used to analyze the fate and transport of non-aqueous phase liquids (NAPLs) in the vadose zone as well as below the water table. The NAPL may consist of a general multicomponent mixture of organic fluids. In addition, one or several non-condensible gases may be present. Any and all phase compositions in a gas-water-NAPL system are treated, including single, two-phase, and three-phase conditions. Flows can be non-isothermal, and may involve advective, diffusive, phase-partitioning, and sorptive processes.&#x20;

In the TMVOC formulation, the multiphase system is assumed to be composed of water, non-condensible gases (NCGs), water-soluble volatile organic chemicals (VOCs), and optional tracers. The number and nature of NCGs and VOCs can be specified by the user. There are no intrinsic limitations to the number of NCGs or VOCs in the TMVOC formulation; Current default total number of components are 20 (ComponentNum=20).  NCGs may be selected by the user from a data bank provided in TMVOC; currently available choices include O2, N2, CO2, CH4, H2, ethane, ethylene, acetylene,   hydrogensulfide, ammonia and air (a pseudo-component treated with properties averaged from N2 and O2).  Thermophysical property data for VOCs must be provided by the user. The fluid components may partition (volatilize and/or dissolve) among gas, aqueous, and NAPL phases. Any combination of the three phases may be present, and phases may appear and disappear in the course of a simulation. In addition, VOCs may be adsorbed by the porous medium, and may biodegrade according to a simple half-life model or using a more complex biodegradation reaction model.

TMVOC allows flow system in any one of the three phases (Gas, aqueous, oil/NAPL phase) or combination of them.  Each phase flows in response to pressure and gravitational forces according to a multiphase extension of Darcy’s law, which includes effects of relative permeability and capillary pressure between the phases. Transport of the mass components may also occur by molecular diffusion in all phases. Multiphase diffusion is treated in a fully-coupled manner that can cope with diffusion of phase-partitioning components under conditions of variable phase saturations.&#x20;

Depending on thermodynamic conditions and relative abundance of the different components, the fluids may exist in seven different phase combinations, as shown in Figure 23. Arrows denote routes for appearance or disappearance of phases that are checked after each update of thermodynamic conditions during the Newton-Raphson iteration process.&#x20;

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption><p>Figure 23. Phase compositions and phase changes considered by TMVOC. The phase designations are: g - gas, w - aqueous, n - NAPL</p></figcaption></figure>

Details for assumptions, physical processes, fluid properties, and phase partitioning for TMVOC module can be found in the original [TMVOC user manual](https://tough.lbl.gov/assets/files/Tough3/TMVOC\_Users\_Guide.pdf).&#x20;

2. **Specifications**

A summary of TMVOC specifications is given in Table 15. The default number of mass components is 2 (water and one gas). The maximum number of components is 20.  The flow system can be in any one of the seven phase conditions.  The component numbering is based on the number of gases, hydrocarbons, and tracers in the model. The first component is always water; the second component is gas1; the third component is gas2; the first hydrocarbon is number (1+NumGases+1) component; the second hydrocarbon is number (1+NumGases+2) component; the first tracer is number (1+NumGases+NumHyC+1) component; the second tracer is number (1+NumGases+NumHyC+2) component. The selection of primary variables uses following rules:

(1) The first primary variable is always the phase pressure (if multiple phases, it is the lighter phase pressure).

(2) The last primary variable is always temperature.

(3) For single phase conditions, primary variables from second are mole fractions of the gases, mole fractions of the hydrocarbon, and mole fraction of tracers, respectively.

(3) For two phase conditions, the second primary variable is the saturation of lighter phase.  Primary variables from third are mole fractions (in the lighter phase) of the gases (starting from second gas), mole fractions of the hydrocarbon, and mole fraction of tracers, respectively.

(4) For three phase condition, the rule (3) is applied except the primary variable for mole fraction of last hydrocarbon is replaced by water saturation ( $$S_a$$) . &#x20;

Table 15 Summary for TMVOC

<table><thead><tr><th width="248">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) Gases (1, ....., NumGas) (2-NumGas are optional)</p><p>(3) Hydrocarbons (1, ......, NumHyC) (optional)</p><p>(3-7) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) Oil, OIL</p><p>(4) Aqueous-Gas, G_A</p><p>(5) Oil-Gas, G_O</p><p>(6) Aqueous-Oil, O_A</p><p>(7) Three Phase, GOA</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/tmvoc.md">Table 28</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation. </td></tr></tbody></table>

3. **Specific input requirements**

TMVOC simulation requires definition gas, hydrocarbon, and tracer components. They are defined through keywords "[GASES](../preparation-of-model-input/keywords-and-input-data/gases.md)", "[CHEMP](../preparation-of-model-input/keywords-and-input-data/chemp.md)" and " [TRACR](../preparation-of-model-input/keywords-and-input-data/tracr.md)", respectively. Details can be found from the inputs for these keywords. If no gas is defined in a simulation, the default gas "AIR" will be included as the gas component. TMVOC does not require other specific input. The following inputs may be required, but are optional.

**IE(402)**               selection of air solubility model

\=0                         use model by D'AMORE AND TRUESDELL (1988), CRAMER (1982)

\=1                           use constant air solubility, $$HC=1.0 \times 10^{-10}$$                                    &#x20;

**IE(403)**               selection of component fraction unit in the simulation. The initial conditions must be consistent with the selection, and the source/sinks are also consistent with the selection. If mass fraction is selected, injection or production rate must be in kilograms. Otherwise, the injection or production rate must be in moles

\=0                          use mole fraction (default).&#x20;

\=1                           use mass fraction.
