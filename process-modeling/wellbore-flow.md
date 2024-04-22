# Wellbore Flow

1. **Description**&#x20;

Wellbore simulation was based on the T2WELL (Pan, et al. 2010).  There are several versions of T2WELL for different EOS modules. In TOUGH4, wellbore simulation is generalized for any EOS modules and fully integrated into the simulator.&#x20;

The approach we use for describing wellbore flow is based on the drift-flux model (DFM) (Shi et al., 2005) for transient two-phase non-isothermal flow. Conservation equations for mass, momentum and energy under different flow regimes in the wellbore are solved numerically while wellbore heat transmission is handled semi-analytically.  The discussion of these equations can be found in[ Section 4](../governing-equations/drift-model.md). The current model is designed for simulation of single- and two-phase flows of water-gas mixtures. Three-phase flow is simplified by combining "gas" and "non-aqueous" phases as a single gas phase in solving the velocities of wellbore flow.  The conventional approach for calculating the mixture velocity in the drift-flux model (DFM) is often based on the steady-state pressure loss equation for wellbore flow (Brill and Mukherjee, 1999). To improve simulation performance in well-bore flow processes involving high fluxes, we have extended the DFM to include the transient terms of the momentum conservation equations in calculating the velocity from the pressure gradient.

In solving the mass and energy balance equations, the mass and energy flux terms need to be calculated at each Newtonian iteration from the most recently updated primary variables. Within the wellbore at each iteration, we calculate the mixture velocity using equation (4-45) first, and then calculate the gas velocity (Eq. 4-46). As for marching in time, the momentum conservation equation (Eq. 4-48) is solved semi-explicitly as

$$u^{n+1}=\dfrac{DR^{n+1}+\frac{1}{\Delta t}\rho^nu^n-(\dfrac{\partial \rho u^2}{\partial L})^n}{\dfrac{\rho^n}{\Delta t}+\dfrac{f^n\rho ^n u^n}{4r_w}}$$                                                                           (7-38)

where, the superscripts _n_ and _n+1_ indicate the previous and current time levels, respectively; $$\Delta t$$ is the time-step size, and DR is the total driving force given by

$$DR=-\dfrac{\partial P}{\partial L}-\rho gcos \theta$$                                                                                                   (7-39)

Normally, the pressure gradient caused by elevation change contributes from 80 to 95% of the total pressure gradient and the friction loss represents 5 to 20%, whereas the acceleration component is normally negligible and can become significant only if a compressible phase exists at relatively low pressures (Brill and Mukhmerjee, 1999). Therefore, the solution of Eq. 7-38 is more like an implicit formulation considering the above-normal pressure gradient components.

When the system reaches a steady state, Eq. 4-48 will be reduced to the pressure loss equation by

$$-\dfrac{dP}{dL}=\dfrac{f\rho u^2}{4r_w}+\rho u \dfrac{du}{dL}+\rho g cos\theta$$                                                                                (7-40)

With the velocities calculated from the above equations, the fluid and heat fluxes between two adjacent well nodes, which are needed in calculation of mass/energy balances, can be obtained by

mass flux:

$$F_{ij}^k=A_{ij}\displaystyle\sum_{\beta}(\rho _\beta X_\beta^k)_{ij+1/2}u_{\beta, ij}$$                                                                                    (7-41)

The total heat flux along the connection of nodes _i_ and _j_, including advective and radial heat conduction terms, may be evaluated by

$$F_{ij}^{h}=\displaystyle\sum_\beta [(\rho_\beta h_\beta)_{ij+1/2}u_{\beta, ij}$$                                                                                           (7-42)

and heat loss/gain by lateral wellbore heat transmission is given by

$$Q_i^h=-A_{wi}(K_{wi})[\dfrac{T_i-T_{\infty (z)}}{f(t)}$$                                                                                      (7-43)

where $$A_{wi}$$ is the lateral area between wellbore and surrounding formation; $$K_{wi}$$ is thermal conductivity (or overall heat transfer coefficient) of wellbore/formation; $$T_{\infty}(z)$$ is ambient temperature; and _f(t)_ is Ramey’s well heat loss function (Ramey 1962):

$$f(t)=\dfrac{1}{-ln(\dfrac{r}{2 \sqrt{\alpha t} })-0.29}$$                                                                                         (7-44)

where α is the thermal dispersivity of the surrounding formation.

In evaluating the flow terms in Eqs. 7-41 and 7-42, subscript _ij + 1/2_ is used to denote a proper averaging or weighting of advective mass transport or heat transfer properties at the interface or along the connection between two blocks or nodes _i_ and _j_ (_j = i - 1_ or _i + 1_). In addition, fully upstream weighting should be used in Eqs. 7-41 and 7-42 for numerical stability.  With the calculated fluxes, the same discrete nonlinear equations (Eqn. 5-7) as other non-wellbore elements are used for mass balance calculation.&#x20;

2. **Input requirements**

To evoke a wellbore simulation, users need to input well parameters through keyword "[WELLB](../preparation-of-model-input/keywords-and-input-data/wellb.md)" and also need to turn on the wellbore simulation through keyword "[MODDE](../preparation-of-model-input/keywords-and-input-data/modde.md)", by setting parameter _hWBM_ in record MODDE.3 to TRUE_._ In addition, the domain (rock) name for the wellbore cells must start with the letter "w" or "x", where "w" indicates normal (open) wellbore cells whereas "x" indicates the special wellbore cells either filled with porous medium or consisting of a bundle of smaller tubes. Wellbore cells are identified by the first character of their rock name ("w" or "x"). Multiple wellbores or multiple branches of a wellbore are allowed. The first cell of each wellbore must have a cell name starting with the character "#" or "\*". The wellhead section must always be defined as the first wellbore cell.&#x20;

T2WELL requires input of several parameters through keyword "SELEC" which is not allowed in TOUGH4 as it may conflict with input of some EOS modules.  Input for these parameters must use keyword "WELLB". In T2WELL, input of some parameters for a specific wellbore section is through assigning special values to a ROCK associated to the section. This may not work anymore. Any parameters for a well section need to be inputted through "WELLB".  For details, users may refer to "[WELLB](../preparation-of-model-input/keywords-and-input-data/wellb.md)".  The original [T2WELL user manua](https://tough.lbl.gov/assets/docs/T2Well\_ECO2N\_Manual.pdf)l may also be very helpful.&#x20;
