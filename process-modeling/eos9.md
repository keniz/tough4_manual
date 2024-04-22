# EOS9

1. **Description**

This module considers variably saturated flow of a single aqueous phase, which consists of a water component and tracers, and neglects phase change effects. The thermophysical properties of water are assumed independent of tracer concentrations. Implicit in this approximation is the assumption that the tracer concentrations are small. The gas phase is treated as a passive bystander at constant pressure, and conditions are assumed to be isothermal. Thus, no mass balance equation for gas and no heat balance is needed, and only a single water mass balance equation is solved for each grid block if no tracer is included. This is very efficient numerically, making EOS9 the module of choice for problems for which the underlying approximations are applicable.

&#x20;Liquid flow in EOS9 is described as follows:

$$\dfrac{\partial}{\partial t}\phi\ S_l\rho_l=\ div\left[k\frac{k_{rl}}{\mu_l}\rho_l\nabla\left(P_l+\rho_lgz\right)\right]$$                                                                          (7-23)                                                              &#x20;

&#x20;where $$\phi$$ is porosity, $$S_l$$ is water saturation,  $$\rho_l$$is water density, _k_ is absolute permeability, $$k_{rl}$$is relative permeability to the aqueous phase, $$\mu_l$$is water viscosity, $$P_l$$is water pressure, _g_ is acceleration of gravity, and _z_ is defined positive upward. Neglecting variations in liquid phase density and viscosity, as is appropriate for (nearly) isothermal conditions, Eq. 7-23 simplifies to Richards’ equation (1931)

$$\frac{\partial}{\partial t}\theta=\ div\left[K\nabla h\right]$$                                                                                                             (7-24)

&#x20;where $$\theta=\phi S_l$$ is specific volumetric moisture content, $$K=\frac{kk_{rl}\rho_lg}{\mu_l}$$ is hydraulic conductivity, and $$h=z+P_l/\rho g$$ is the hydraulic head. EOS9 can describe flow under partially saturated (_0 < Sl < 1_) as well as fully saturated conditions, and phase changes between the two.

2. **Specifications**

A summary of EOS9 specifications is given in Table 12.  The default number of mass component is 1. Simulation can only be run in isothermal. With only a single mass balance equation per grid block (not considering tracers), there is only a single primary thermodynamic variable. This is taken to be pressure for single-phase (saturated) conditions, and is water saturation for unsaturated conditions. A distinction between the two is made simply on the basis of the numerical value of the first primary variable, $$X_l$$. If  $$X_l$$ _< 1_, this indicates that  $$X_l$$represents water saturation and conditions are unsaturated; if  $$X_l$$ is larger than a user-specified gas phase reference pressure (default $$P_{gas} = 1.013\times10^5 Pa$$), it is taken to be water pressure, and saturated conditions prevail. When phase changes between saturated and unsaturated conditions occur, the primary variable is switched, as follows. The numerical value of  $$X_l$$and its change during the Newton-Raphson iteration process is monitored. If  $$X_l$$ changes from being smaller than 1 to larger than 1, this indicates attainment of fully saturated conditions. In that case $$X_l$$ is switched to pressure, and is initialized at a pressure slightly in excess of gas phase reference pressure as $$X_l=P_{gas}(1+\varepsilon)$$, with $$\varepsilon=10^{-6}$$. If  $$X_l$$ changes from being larger than $$P_{gas}$$ to smaller than  $$P_{gas}$$, this indicates a transition from fully to partially saturated conditions.  $$X_l$$is then switched to saturation, and is initialized as $$X_l=1-\varepsilon$$_._ Actually, a transition from fully to partially saturated conditions is made only when  $$X_l$$ drops below $$P_{gas}(1-\varepsilon)$$; test calculations have shown that such a (small) finite-size window for phase change improves numerical stability and efficiency. If tracers exist, one additional primary variable is needed for each tracer. It always takes the tracer mass fraction in liquid water as the primary variable. &#x20;

Table 12 Summary for EOS9

<table><thead><tr><th width="295">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2-6) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Unsaturated, USA </p><p>(2) Saturated, SAT </p><p></p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eos9.md">Table 25</a></td></tr><tr><td>Optional process modeling</td><td>Wellbore simulation, and Biodegradation reactions. </td></tr></tbody></table>

In EOS9, the thermophysical properties of water are taken at default reference conditions of _P =_ $$1.013\times10^5$$ Pa_, T_ = 15 ˚C. These defaults can be overwritten in a flexible manner by specifying appropriate data in a fictitious[ ROCKS](../preparation-of-model-input/keywords-and-input-data/rocks.md) domain ‘REFCO’, as follows.

&#x20;     reference pressure:         DROK of REFCO

&#x20;     reference temperature:  POR of REFCO

&#x20;     liquid density:                   PER(1) of REFCO

&#x20;     liquid viscosity:                PER(2) of REFCO

&#x20;     liquid compressibility:    PER(3) of REFCO

Note that assignment of thermophysical data through a specially-named domain was set up just as a convenient way of providing floating-point parameters to the code. No volume elements (grid blocks) should be attached to domain ‘REFCO’, as the data in general will not correspond to reasonable hydrogeologic parameters. The above-mentioned defaults will be overwritten for any parameters for which a non-zero entry is provided in ‘REFCO’. This allows the generation of these parameters internally for user-defined (_P, T_); it also allows for directly assigning user-desired values as, e.g., $$\rho_{liq}$$= 1000 kg/m3, $$\mu_{liq}=10^{-3}$$Pa-s (=1 centipoise), etc.&#x20;

In addition to specifying the primary thermodynamic variable on a default, domain, or grid block basis, EOS9 offers alternative ways of initializing flow problems. The primary variable may be entered as a negative number upon initialization, in which case it will be taken to denote capillary pressure, and will be internally converted to $$S_l$$ in the initialization phase. EOS9 can also initialize a flow problem with gravity-capillary equilibrium, relative to a user-specified reference elevation $$z_{ref}$$ of the water table. This type of initialization will be engaged if the user enters a non-zero number in slot CWET in ROCKS domain ‘REFCO’, in which case CWET will be taken to denote the water table elevation $$z_{ref}$$, in units of meters. Water pressure at$$z_{ref}$$is taken equal to reference gas pressure, $$P_l(z_{ref})=P_{gas}$$, and is initialized as a function of grid block elevation according to $$P(z)=P_{gas}+(z_{ref}-z)\rho g$$. By convention, the z-axis is assumed to point upward. In order to use this facility, the z-coordinates (grid block elevations) must be specified in the ELEME-data, which will be done automatically if internal MESH generation is used.

In the assignment of gravity-capillary equilibrium as just discussed, water saturations at “sufficiently” high elevations above the water table may end up being smaller than the irreducible water saturation $$S_{lr}$$specified in the relative permeability function, which may or may not be consistent with the physical behavior of the flow system. Users may optionally enforce that $$S_l=S_{lr}$$ in regions where the capillary pressure function would dictate that $$S_l<S_{lr}$$ . This is accomplished by entering an appropriate parameter in slot SPHT of ROCKS domain ‘REFCO’, and works as follows. The irreducible saturation  $$S_{lr}$$ will be taken to be parameter RP(int(SPHT)) of the relative permeability function. As an example, for the IRP _=_ 7 relative permeability function, irreducible water saturation is the parameter RP(2); therefore, for IRP _=_ 7 the user should specify SPHT _=_ 2.0 in ‘REFCO’ to use this facility.
