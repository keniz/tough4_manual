# EOS7

1. **Description**&#x20;

Geologic carbon sequestration, compressed air energy storage, underground hydrogen storage, and many other subsurface energy-related engineering applications involve transport of multiple gases and their mixtures in subsurface geologic media. TOUGH4/EOS7 was designed for these types of applications. It covers the original EOS7, EOS7R, EOS7C, and EOS7CA modules in TOUGH3. It is for multicomponent gas mixtures with or without an aqueous phase and H2O vapor. Components for the new EOS7 modules can include water, brine, a choice of non-condensable gases, selected tracers, and optional heat. The gas components can be any combination of 1-4 gases of the seven available gases (CH4, H2S, CO2, N2, O2, H2, and AIR). The EOS7 module uses a cubic equation of state and an accurate solubility formulation along with a multiphase Darcy’s Law to model flow and transport of gas and aqueous phase mixtures over a wide range of pressures and temperatures appropriate to typical subsurface gas/energy storage sites and natural gas reservoirs. The real gas properties module has options for Peng-Robinson, Redlich- Kwong, or Soave-Redlich-Kwong equations of state to calculate gas mixture density, enthalpy departure, and viscosity. Solubility of gases is calculated using a very accurate chemical equilibrium approach. Transport of the gaseous and dissolved components is by advection and Fickian molecular diffusion.

EOS7 represents the aqueous phase as a mixture of (pure) water and brine. This approach is very useful for flow problems in which salinity does not reach saturated levels (Reeves et al., 1986; Herbert et al., 1988). The salinity of the aqueous phase is described by means of the brine mass fraction, $$X_b$$, and density and viscosity are interpolated from the values for the water and brine endmembers. Salinity-dependent gas solubility is also taken into account, but no allowance is made for reduction of vapor pressure with salinity. The brine is modeled as NaCl solution, and the non-condensible gas is the selected gas or gas mixture. The representation of the temperature and pressure dependence of thermophysical properties is somewhat more general than that of Reeves et al. (1986), retaining the flexibility of the TOUGH formulation for nonisothermal processes.

EOS7 can describe phase conditions ranging from single-phase liquid to two-phase to single-phase gas. However, the approach of describing variably saline fluids not as mixtures of water and salt but as mixtures of water and brine has specific limitations which need to be considered in applications. It does not allow existence of solid salt. From a physical viewpoint brine mass fraction in the gas phase should always be equal to zero, but the only way the brine mass balance can be maintained during phase transitions from two-phase to single-phase vapor conditions is by allowing $$X_b$$, gas to vary freely. Users need to carefully examine problem setups and results to guard against unphysical results in applications that involve boiling. We now briefly summarize the treatment of thermophysical properties in EOS7.

_(1) Brine properties_

In TOUGH4, a general-purpose module for brine properties was developed which can be used in any EOS modules involving brine.&#x20;

In the brine property module, the density of the aqueous phase is calculated from the assumption, shown to be very accurate by Herbert et al. (1988), that fluid volume is conserved when water and brine are mixed. Mixture density $$\rho_m$$can then be expressed in terms of water and brine densities as follows.

$$\dfrac{1}{\rho_m}=\dfrac{1-X_b}{\rho_w}+\dfrac{X_b}{\rho_b}$$                                                                                                 (7-7)

where $$\rho_w$$and $$\rho_b$$ are water and brine density, respectively. Eq. 7-7 applies to densities at fixed pressure and temperature conditions. In order to achieve a simple approximation for fluid density at variable temperatures and pressures, EOS7 takes compressibility and expansivity of brine to be equal to those of water. This will provide a reasonable approximation at least for a limited range of temperatures and pressures around the reference conditions$$(P_0, T_0)$$. The default reference brine has a density of 1185.1 _kg/m3_ at reference conditions of $$P_0=1$$bar, $$T_0$$ = 25 ˚C, corresponding to an NaCl solution of 24.98 wt-%, or 5.06 molar (Potter and Brown, 1977; cited after Finley and Reeves, 1982). The user may specify different reference conditions and brine densities. Effects of salinity on the enthalpy of the aqueous phase are ignored.

Following Herbert et al. (1988), salinity effects on aqueous phase viscosity are modeled with a polynomial correction to the viscosity of pure water. Mixture viscosity $$\mu_m$$is represented as follows.

$$\mu_m\left(P,T,X_b\right)=\mu_w\left(P,T\right)\cdot f\left(X_b\right)$$                                                                     (7-8)

where

$$f\left(X_b\right)=1+v_1X_b+v_2{X_b}^2+v_3{X_b}^3$$                                                                   (7-9)

with default values of $$v_1$$= 0.4819, $$v_2$$ = -0.2774, and $$v_3$$ = 0.7814. Different values for the coefficients may be specified by the user.&#x20;

_(2) Gas properties_

TOUGH4 rewrote the real gas property module based on a set of subroutines contained within a submodule called ZEVSREAL (a.k.a. GasEOS in its stand-alone form), where ZEVS stand for Z factor, Enthalpy, Viscosity, and Solubility, and REAL refers to the fact that the module calculates properties of real gas mixtures. The new real gas property module is generalized for combinations of any included gases and calibrated for better accuracy. It is parallelized with OPENMP and ready for use in any EOS module.&#x20;

The real gas property module uses a cubic equation of state to calculate properties of real gas mixtures. Air is specially treated as a pseudo-component (AIR) with properties reflecting a mixture of two gas components, i.e., 79% N2 and 21% O2 (by volume), in solving the selected real gas cubic equation of state.

_Density_

The real-gas property module calculates mixture properties using cubic equations of state, so-named because the volume terms are raised to either the first, second, or third power (Reid et al., 1987). The most common two-parameter equations of state can be written as

$$P=\dfrac{RT}{V-b}-\dfrac{a}{V^2+ubV+wb^2}$$                                                                         (7-10)&#x20;

where the parameters and functions _u, w, b,_ and _a_ take on different values depending on the particular cubic equation of state being used, _T_ is temperature in degrees K, _V_ is gas volume, _P_ is pressure, and _R_ is gas constant. EOS7 provides the option for Peng-Robinson (PR), Redlich-Kwong (RK), or Soave-Redlich-Kwong (SRK) depending on user choice. However, our experience is that the Peng-Robinson equation of state is very accurate for CO2-CH4 systems and N2-CH4 systems, but is very inaccurate for gas mixtures including H2. Readers interested in more detail in the range of applicability of Eq. 7-10 and recommendations on the use of various equations of state should consult Reid et al. (1987) and Poling et al. (2000) for more information. We use the Peng-Robinson equation of state as an example for the following discussions.

The approach taken in EOS7 is to use the Peng-Robinson equation of state to calculate the _Z_ factor of the mixture, where

$$PV=ZnRT$$                                                                                                             (7-11)

From this value, the density of the gas mixture can be calculated using

$$\rho=\dfrac{M_Wn}{V}=\dfrac{PM_W}{ZRT}$$                                                                                                (7-12)

where$$M_w$$is the molecular weight of the real gas mixture and _n_ is the gas molar number.

_Enthalpy_

The enthalpy of the real-gas mixtures is calculated using an ideal gas value with an added enthalpy departure to account for real gas effects. Real gas mixtures depart from ideality in ways that can be modeled with cubic equations of state. Following equation is use for the calculation:

$$H=(H-H^{ig})+H^{ig}=(H-H^{ig})+\displaystyle\sum_iX^iH^{i,ig}$$                                         (7-13)

where $$(H-H^{ig})$$ is the enthalpy departure. TOUGH4 uses cubic equations of state (e.g., Peng- Robinson) to calculate the enthalpy departures and ideal gas enthalpy change to come up with the total enthalpy change of the real gas mixture.

Water property module in TOUGH4 uses real-gas properties (steam tables) for steam enthalpy, and thus produces more accurate steam enthalpies than the cubic equations of state can provide. As an alternative, the user may choose (see following sub-section 2 for specific input requirement) to use the steam tables to calculate the enthalpy of the steam (water vapor) fraction in the gas, and use real gas property module to calculate the enthalpy of the other gases mixture. The total gas mixture enthalpy is then calculated as a weighted combination of their contributions.

Specifically, in order to match enthalpies from the NIST Chemistry Web Book (NIST, 2013), the calculated enthalpies need to be adjusted. Table 3 shows the adjustment amount for different gas components. After adjustment, the model provides accurate enthalpy estimates relative to NIST values for the single gas components, with the maximum error less than 1% (using SRK).

&#x20;Table 10. Adjustment amount for the enthalpy calculation

| Gas Name | Adjustment amount (J/kg) |
| -------- | ------------------------ |
| CH4      | 862300                   |
| H2S      | 608600                   |
| CO2      | 481900                   |
| N2       | 283300                   |
| O2       | 248200                   |
| H2       | 3587800                  |
| AIR      | 277900                   |

&#x20;_Viscosity_

The method of Chung et al. (1988) as described in Reid et al. (1987) and Poling et al. (2000), originally implemented in TOUGH3/EOS7C, is accurate to within 5-10% for most gases at common reservoir conditions. However, it is inaccurate for estimating viscosity of mixtures that include hydrogen (H2). To remedy this, we implemented the method of Quinones et al. (2001; 2000) in TOUGH4. In this method, viscosities of the pure gas or gas mixtures were calculated with the correlation developed from friction theory in conjunction with the cubic equation of state. Detailed discussion of the implementation and calibration of this method can be found at Cai et al. (2022). The key parameters for this method (friction coefficients) were calculated using friction constants through regression as in Zéberg-Mikkelsen et al. (2001a, 2001b). For CO2, the friction coefficients were estimated from the general one-parameter model (Quinones et al. 2001). Compared to NIST values, this method underestimates the dynamic viscosity for some gases in high-pressure cases if directly using the friction coefficient values of the pure gas component provided by Zéberg -Mikkelsen et al. (2001a). To address this, the model was calibrated to improve accuracy of the viscosity calculation through adjusting the friction coefficient values and other terms. Verification of the calibrated model against lab measurements and NIST database results shows accurate viscosity estimates are obtained using this calibration.

_Solubility_

The model for mutual solubility of gas mixture components in the aqueous phase was based on local thermodynamic equilibrium as described by Oldenburg et al. (2004) in TOUGH3/EOS7C. In the original approach, partitioning of the gas components between the gaseous and aqueous phases is calculated using an accurate effective Henry’s coefficient (_Kh_) and the primary variables of gas mass fraction in the liquid. In order to solve the cubic equation of state to obtain an accurate compressibility factor (Z) needed to calculate gas density, it is assumed gas phase mole fractions are known and mole fractions are a function of the effective Henry’s coefficient. Therefore, an iterative approach is required wherein the first guess of _Kh_ to estimate gas-phase concentrations from known liquid-phase concentrations is taken from the models of Cramer (1982), and D’Amore and Truesdell (1988).  In TOUGH4, the same approach is used. However, to avoid the iterative procedure required in TOUGH3/EOS7C, a different set of primary variables with gas mass fractions excluding water vapor in the gaseous phase for two-phase system are used.

The method of computing the partitioning of the NCG between aqueous and gas phases is presented here using CO2 as an example, but the same treatment can be used for other gases. Note that the effects of brine on aqueous phase solubility are not included in the present following formulations. We begin by writing the equation for the dissolution and exsolution of CO2 in the aqueous phase as

$$CO_2(g)\iff CO_2(aq)$$                                                                                             (7-14)

the equilibrium constant for which is given by

$$K_{CO_2(g)}=\dfrac{aCO2_2}{f_{CO_2}}$$                                                                                                       (7-15)

where _a_ is the activity which refers to the aqueous phase and _f_ is the fugacity which refers to the gas phase. The Poynting Correction accounts for the change in equilibrium constant due to pressure change (Prausnitz et al., 1986) and can be written as

$$K_{T,P}=K_{T,P^0}^0exp(\dfrac{(P-P^0)\overline{V_i}}{RT})$$                                                                               (7-16)

where the equilibrium constant ( $$K_{T,P^0}^0$$) at reference pressure ( $$P_0$$) of 1 bar can be taken from the literature or fitted to experimental data (Spycher et al., 2003). We define the activity of CO2 in the aqueous phase as a function of activity coefficient and molality as

$$a_{CO2}=\gamma m_{CO2}$$                                                                                                             (7-17)&#x20;

Assuming the activity coefficient to be equal to one, the mole fraction of CO2 in the aqueous phase is given by

$$x_{aq}^{CO2}=\dfrac{a_{CO2}}{55.508}$$                                                                                                             (7-18)

assuming there are 55.508 moles H2O per kg of aqueous phase. The fugacity of CO2 can be written

$$f_{CO2}=\phi_{CO2}y_g^{CO2}P^t=\dfrac{a_{CO2}}{K_{CO2(g)}}$$                                                                                 (7-19)        &#x20;

where $$\phi$$ is the fugacity coefficient, $$y_g$$ is the mole fraction in the gas phase, and $$P^t$$is the total gas pressure. Combining Eqs. 7-15, 7-18, and 7-19, we have an expression for the equilibrium constant

$$K_{CO2(g)}=\dfrac{55.508x_{aq}^{CO2}}{\phi_{CO2}y_g^{CO2}P^t}$$                                                                                              (7-20)

For CO2, if _T_ < 100 °C, we use partial molar volumes of Spycher et al. (2003) for calculating the equilibrium constant of Eq. 7-20 in the real gas property module. For other components and temperatures, we use SUPCRT92 (Johnson et al., 1992) and the slop98 database of Shock and Plyasunov (2004) to calculate equilibrium constants.

From the definition of partial pressure, the equilibrium constant of Eq. 7-20, and a Henry’s Law type relation, we can define an effective Henry’s coefficient from

$$P^{CO2}=y_g^{CO2}P^t=\dfrac{55.508x_{aq}^{CO2}}{K_{CO2(g)}\phi_{CO2}}=Kh_{CO2}x_{aq}^{CO2}$$                                                    (7-21)

&#x20;where the effective Henry’s coefficient (_Kh_) is given by

$$Kh_{CO2}=\dfrac{55.508}{K_{CO2(g)}\phi_{CO2}}$$                                                                                               (7-22)

The accurate Henry’s coefficients given by Eq. 7-22 are used to calculate partitioning of the gas components in the gas and aqueous phases.&#x20;

The impact of salinity on the _Kh_ is considered in EOS7. Salinity-dependence of $$Kh^{gas}$$was included by increasing $$Kh^{gas}$$in aqueous solutions with higher brine mass fractions. It is assumed the same effects of brine on air solubility occur also for NCG and tracer components. For example, if the Henry’s Law coefficient for air in pure water and in brine at the local brine concentration are $$Kh_{H2O}^{air}$$ and $$Kh_{brine}^{air}$$, respectively, then the Henry’s Law coefficient for NCG in pure water at a given temperature would be multiplied by the ratio $$Kh_{brine}^{air}/Kh_{H2O}^{air}$$ to obtain the value for the NCG Henry’s Law coefficient at the given brine mass fraction.&#x20;

(3) Tracers

Discussions for the simulation of tracers are presented in the section [Decay Chain/Tracers](tracers-decay-chain.md).&#x20;

2. **Specifications**

A summary of EOS7 specifications and parameters is given in Table 11. The default number of mass components is 2 (water and one user selected gas). The maximum number of components is 11.  The default choice of primary thermodynamic variables is (P, Xg, T) for single-phase, (Pg, Sg + 10, T) for two-phase conditions. The last primary variable is always temperature no matter if the simulation is in isothermal or non-isothermal, but in isothermal simulation the energy equation does not need to be solved and temperature is always constant. The component numbering is based on the number of gases and tracers included in the simulation. For example, gas1 is always component 2, gas2 is component 3, gas3 is component4, and component 4 is component 5. If the model has 1 gas, 2 gases, 3 gases or 4 gases, the brine will be component 3, 4, 5, 6 respectively.  The component number of a tracer is the component number of brine plus the numbering of the tracer.&#x20;

Table 11 Summary for EOS7

<table><thead><tr><th width="248">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) Gases (at least 1 gas, at most 4 gases, gas 2-4 is optional)</p><p>(3) Brine</p><p>(4-8) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) two-phase, AQG</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eos7.md">Table 24</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation. </td></tr></tbody></table>

3. **Specific input requirements**

EOS7 allows inputs of several optional parameters through keyword "[SELEC](../preparation-of-model-input/keywords-and-input-data/selec.md)", including:

Record **SELEC.2**

&#x20;                     Format (3E10.4) or free format (data separated by comma)

&#x20;                     $$P_0, T_0, \rho_b$$    (FE(1)-FE(3))

$$P_0$$                 reference pressure for brine property calculation, Pa

$$T_0$$                 reference temperature for brine property calculation, $$^oC$$

$$\rho_b$$                  brine density at $$(P_0. T_0) ,  kg/m^3$$           &#x20;

If any of these parameters is entered as zero, default values of $$P_0$$ = 1 bar, $$T_0$$= 25 ˚C, $$\rho_b$$ = 1185.1 kg/$$m^3$$ will be used. For $$P_0$$ < 0, brine properties will be assumed identical to water.

&#x20;                     Format (3E10.4) or free format (data separated by comma)

&#x20;                     $$v_1, v_2, v_3$$    (FE(9)-FE(11))

coefficients for salinity correction of aqueous phase viscosity, see Eq. 7-9.

EOS7 requires definition for gases and tracers which are included in the simulation. The inputs for gas definition are by keyword "[GASES](../preparation-of-model-input/keywords-and-input-data/gases.md)", and tracer definition is by keyword "[TRACR](../preparation-of-model-input/keywords-and-input-data/tracr.md)".&#x20;

Users are also allowed to use the specific input requirement for EOS7R/EOS7C/EOS7CA of TOUGH3 for diffusion coefficients, gas and tracer parameters through keyword "SELEC". Please refer to the user manual of TOUGH3-[EOS7R](https://tough.lbl.gov/assets/docs/TOUGH2\_EOS7R\_Users\_Guide.pdf)/[EOS7C](https://tough.lbl.gov/assets/docs/TOUGH2-EOS7C\_Users\_Guide.pdf)/[EOS7CA](https://tough.lbl.gov/assets/docs/TOUGH2-EOS7CA\_Users\_Guide.pdf) for details. These specific inputs will be effect in TOUGH4 only when the input type specified through parameter "InitCType" is "EOS7R, EOS7C, or EOS7CA.  "InitCType" is in the first record of keyword "[MODDE](../preparation-of-model-input/keywords-and-input-data/modde.md)"
