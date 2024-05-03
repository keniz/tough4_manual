# ECO2

1. **Description**

ECO2 is a fluid property module designed for applications to geologic storage of CO2 in saline aquifers. It includes a comprehensive description of the thermodynamics and thermophysical properties of H2O-NaCl-CO2 mixtures, that reproduces fluid properties largely within experimental error for temperature, pressure and salinity conditions in the range of  $$10^oC<T<300 ^oC$$, _P_<600 bar, and salinity from zero up to full halite saturation. TOUGH4/ECO2 combines the ECO2N, ECO2M and ECO2N V2 modules in TOUGH3 into a single module and provides the option to run the simulation in two-phase or three-phase conditions.&#x20;

ECO2 can model the same fluid components (water, NaCl, and CO2) as modeled by TOUGH3/ECO2N, ECO2M and ECO2N V2.  In addition, it also allows to include as many as 5 tracers in the simulation. In the two-component system water-CO2, at temperatures above the freezing point of water and not considering hydrate phases, three different fluid phases may be present: an aqueous phase that is mostly water but may contain some dissolved CO2, a liquid CO2-rich phase that may contain some dissolved water, and a gaseous CO2-rich phase that also may contain some water. Altogether there may be seven different phase combinations (Figure 19). If NaCl (“salt”) is added as a third fluid component, the number of possible phase combinations doubles, because in each of the seven phase combinations depicted in Figure 19 there may or may not be an additional phase consisting of solid salt. Liquid and gaseous CO2 may coexist along the saturated vapor pressure curve of CO2, which ends at the critical point $$(T_{crit}, P_{crit})$$= (31.04 °C, 73.82 bar; Vargaftik, 1975), see Figure 20. At supercritical temperatures or pressures there is just a single CO2- rich phase. &#x20;

ECO2 can represent all of the phase conditions and transitions depicted in Figure 19. It may therefore be applied to flow systems that involve both sub- and supercritical temperature and pressure conditions, as well as transitions between them. ECO2 also provides an option by treating the liquid and gas CO2 as a single phase to simplify the simulation (equivalent to TOUGH3/ECO2N).&#x20;

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="296"><figcaption><p>Figure 19. Possible fluid phase combinations in the system water-CO2, and transitions between them in the P-T range of ECO2. The phase designations are a - aqueous, l - liquid CO2, g - gaseous CO2. Separate liquid and gas phases of CO2 exist only at subcritical conditions. Phase combinations are identified by a numerical index that ranges from 1 to 7.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (41).png" alt="" width="425"><figcaption><p>Figure 20. Phase states of CO2</p></figcaption></figure>

ECO2 inherits all the functionalities in handling phase transitions, treatment of dissolved and solid salts, partitioning of fluid components among phases, and calculation of fluid thermophysical properties, and impact of permeability by precipitation and dissolution.  If there is any conflict of functionalities among these modules, the approaches in ECO2N V2 are adopted, or the program provides an option for user to choose.  Any calculations involved in three-phase simulation will use the approaches provided by ECO2M. Details can be found in the user manual of the previous three EOS modules:

[ECO2N user manual](https://tough.lbl.gov/assets/docs/TOUGH2\_ECO2N\_Users\_Guide.pdf)

[ECO2M user manual](https://tough.lbl.gov/assets/docs/TOUGH2-ECO2M\_Users\_Guide.pdf)

[ECO2N V2 user manual](https://tough.lbl.gov/assets/files/02/documentation/TOUGH2-ECO2N\_V2.0\_Users\_Guide.pdf)

2. **Specifications**

A summary of ECO2 specifications and parameters is given in Table 13. The default number of mass components for this module is 3 (water, CO2 and NaCl). The maximum number of components is 8.   In TOUGH4, the gas component (CO2) is always component 2 (In TOUGH3/ECO2N ECO2M, ECO2N V2, CO2 is component 3).  The flow system can be in 4 phases: gaseous CO2, aqueous, Liquid CO2, and solid salt.  The solid salt is immobile and no flux calculation is needed.&#x20;

In the numerical simulation of brine-CO2 flows, we are concerned with the fundamental thermodynamic variables that characterize the brine-CO2 system, and their change with time in different subdomains (grid blocks) of the flow system. Four primary variables are required to define the default state of water-NaCl-CO2 mixtures, which according to conventional TOUGH usage are denoted by X1, X2, X3, and X4. Depending upon the phase combination present, not all thermodynamic parameters are independent, and different sets of primary thermodynamic variables must be used for different phase combinations (see [Input for Initial Conditions](../preparation-of-model-input/inputs-for-initial-conditions/eco2.md)).  For consistency in TOUGH4, X2 is for fluid saturation or CO2 mass fraction, and X3 is for salt mass fraction or its solid saturation. which is opposite to the case in three EOS modules. In ECO2, it is difficult to identify and distinguish phase compositions based on the values of primary variables. For this reason, the input of phase state index or its name as part of the initial condition is required. &#x20;

Table 13 Summary for ECO2

<table><thead><tr><th width="248">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) CO2 </p><p>(3) NaCl (optional)</p><p>(4-8) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) Liquid, LIQ</p><p>(4) Aqueous-Gas, AQG</p><p>(5) Liquid-Gas, LIG</p><p>(6) Aqueous-Liquid, AQL</p><p>(7) Three Phase, ALG</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eco2.md">Table 26</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation. </td></tr></tbody></table>

$$*$$ Solid salt can exist in any of the seven phase conditions

3. **Specific input requirements**

The specific input requirements for the previous three EOS modules are still allowed by ECO2. Inputs of the parameters through keyword "[SELEC](../preparation-of-model-input/keywords-and-input-data/selec.md)".&#x20;

**IE(8)**              allows choice of the manner in which phase assignments are handled for supercritical temperatures. (Recall that for T >  $$T_{crit}$$, points with P ≥ $$P_{crit}$$are arbitrarily assigned as liquid, points with P <  $$P_{crit}$$ as gas.)&#x20;

0:   the AQL<==> AQG phase transition will always be made, based on comparing P with $$P_{crit}$$.

\>0: the AQL <==> AQG phase transitions for supercritical T will only be made for the first few Newtonian iterations (iteration counter ITER ≤ IE(8)).

**IE(9)**              allows choice of a finite window for certain phase transitions. A “hairtrigger” criterion (see Sec. 2.4, ECO2M user manual) will be applied for ITER < IE(9), while for ITER ≥ IE(9), phase transitions will only be made when pressure P or mass fraction X is outside a finite window.&#x20;

The LIQ ==> LIG and AQL ==> ALG transition will only be made when P < (1 - FE(3)) \* $$P_{s,CO2}$$.&#x20;

The AQG ==> ALG transition will only be made when P > (1 + FE(3)) \*$$P_{s,CO2}$$..&#x20;

The LIQ ==> AQL transition will only be made when X < $$X_{l,eq}$$\* (1 - FE(3)).&#x20;

The AQU ==> AQL transition will only be made when X >$$X_{aq,l}$$\* (1+FE(4)).&#x20;

The AQU ==> AQG transition will only be made when X >$$X_{aq,g}$$\* (1+FE(4)).

**IE(11)**               selects dependence of permeability on the fraction $$\phi_f /\phi_0=(1-S_s)$$ of original pore   space that remains available to fluids.&#x20;

0: permeability does not vary with $$\phi_f$$.&#x20;

1: $$k/k_0=(1-S_s)^\gamma$$, with $$\gamma=FE(1)$$.&#x20;

2: fractures in series, i.e., Eq. (24) in ECO2N user manual with exponent 2 everywhere replaced by 3.&#x20;

3: tubes-in-series, i.e., Eq. (24) in ECO2N user manual.

**IE(13)**              allows choice of dependence of brine density on dissolved CO2.&#x20;

0: brine density varies with dissolved CO2-concentration, according to García's (2001) correlation (Eqs. 13-14) for temperature dependence of molar volume of dissolved CO2.&#x20;

1: brine density is independent of CO2 concentration.

**IE(14)**               allows choice of treatment of thermophysical properties as a function of salinity.&#x20;

0: full dependence.&#x20;

1: no salinity dependence of thermophysical properties (except for brine enthalpy; salt solubility constraints are maintained).

2: no salinity dependence of thermophysical properties including brine enthalpy

**IE(15)**               allows choice of correlation for brine enthalpy at saturated vapor pressure&#x20;

0: after Lorenz et al. (2000).&#x20;

1: after Michaelides (1981).&#x20;

2: after Miller (1978).

**IE(16)**               allows choice of mutual solubility model.

0: mutual solubilities from Spycher and Pruess (2005, 2010).

&#x20;1: exactly the same mutual solubility model for low temperature as implemented in ECO2N (not recommended for systems involving high temperature).

**IE(18)**               turn on/off the impact of permeability change caused by solid precipitation /dissolution in flux calculation&#x20;

0: off

1: on, the changed permeability will be used for calculation of flux between two grids.

**IE(22)**                run ECO2 simulation in (can also be specified in keyword [MODDE.3](../preparation-of-model-input/keywords-and-input-data/modde.md))

0: in three phases

1: in two phases, treat both gas and liquid CO2 as a single gas phase.     &#x20;

**IE(31)**             Selects the effects of water on the thermophysical properties of the CO2-rich phase (for ECO2 only).&#x20;

0: ignore the impact of water on the density and viscosity of the CO2-rich phase.&#x20;

1: fully consider impact of water on the CO2-rich phase thermophysical properties.

\-1: ignore the impact of water on density, viscosity and enthalpy of CO2-rich phase (IE(31)=-1 is compatible with ECO2N v1.0).&#x20;

**IE(34)**             Adjusts calculated CO2 enthalpy using the analytical solution by Altunin et al. (1975) to match the value from NIST Chemistry Web Book

0: no adjustment (compatible with ECO2N V1.0).&#x20;

1: do the adjustment to match NIST reference state (If you use enthalpy data from NIST Chemistry Web Book as input for source/sinks, IE(34) must be 1 ).

**FE(1)**               parameter γ (for IE(11)=1); parameter $$\phi_r$$(for IE(11) = 2, 3)&#x20;

**FE(2)**              parameter $$\Gamma$$ (for IE(11) = 2, 3)&#x20;

**FE(3)** if set to a small non-zero number (e.g., $$10^{-5}$$ to  $$10^{-3}$$), will specify a finite window for some phase changes (see IE(9)).&#x20;

**FE(4)** if set to a small non-zero number (e.g., $$10^{-5}$$ to  $$10^{-3}$$), will specify a finite window for some phase changes (see IE(9)).&#x20;

Simulations with ECO2N, ECO2M and ECO2N V2 in previous TOUGH codes require a data file CO2TAB for providing a table of CO2 thermophysical properties. Properties of pure CO2 contained in CO2TAB are obtained from correlations developed by Altunin et al. (1975). The Altunin's correlations have been implemented in TOUGH4, In a ECO2 simulation, CO2TAB is not essential.  if CO2TAB file does not exist in the working directory, TOUGH4 will create the table for current simulation.  The default CO2 property table generated by TOUGH4 covers following range:

pressure:  1.0e+05 to 7.25e+07 (Pa), divided in 200 points with a constant $$\Delta P$$ .

Temperature: 3.05 to 300.0 ($$^oC$$), divided in 150 points with a constant $$\Delta T$$ .

The default table has a total of 30000 ($$200 \times 150$$) points, Thermophysical properties at any pressure and temperature in the table given ranges can be interpolated from the table. TOUGH4 provides an option for user to define the table by input following parameters:

**FE(50)**             lower bound of pressure range (in Pa). &#x20;

**FE(51)**              upper bound of pressure range (in Pa). &#x20;

**FE(52)**             lower bound of temperature range (in $$^oC$$). &#x20;

**FE(53)**             upper bound of temperature range (in $$^oC$$).

**IE(50)**              number of the pressure points (allow 50-1000).

**IE(51)**               number of the temperature points (allow 50-1000).&#x20;

A reasonable CO2 property table will significantly improve simulation performance and accuracy.  The table may only need to cover the pressure and temperature range that the current model may have, but it must cover the whole CO2 saturation line. &#x20;
