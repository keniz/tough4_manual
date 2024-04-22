# Drift Model

_**Mass and Energy Conservation**_

According to mass and energy conservation principles, the generalized conservation equation of mass components and energy in the wellbore can be written as follows:

$$\frac{{\partial {M^\kappa }}}{{\partial t}} = {q^\kappa } + {F^\kappa }$$                                                                                                          (4-36)

where superscript $$\kappa$$ is the index for the components, $$\kappa$$ = 1 to NumCom, NumCom+1 is energy, taken as internal and kinetic energy here;  $$M^\kappa$$  are the accumulation terms of the components  $$\kappa$$ ;   $$q^\kappa$$   are external source/sink terms for mass or energy components; and  $$F^\kappa$$  are the mass or energy transport terms along the borehole due to advective processes.&#x20;

&#x20;_**Accumulation Terms**_

The accumulation term $$M^\kappa$$   of Eq. 4-36 for the mass components in single- or two- phase system is given by

&#x20;$${M^\kappa } = {\rho _G}{S_G}X_G^\kappa  + {\rho _L}{S_L}X_L^\kappa (\kappa  = 1,NumCom)$$                                                   (4-37)

where $$X^{\kappa}_{\beta}$$ is the mass fraction of component $$\kappa$$ in fluid phase  ( = G for gas;  = L for liquid), $$\rho_{\beta}$$is the density of phase $$\beta$$; and $$S_{\beta}$$ is the local saturation of phase defined as

&#x20;$${S_G} = \frac{{{A_G}}}{A} = \frac{{{A_G}}}{{{A_G} + {A_L}}}$$                                                                                                      (4-38)

&#x20;where _A_ is the well cross-sectional area; $$A_G$$ and $$A_L$$ denote the cross-sectional areas occupied by gas and liquid over the cross section at a given elevation (or distance along the well).  The

accumulation term for energy is defined as

$${M^e} = \sum\limits_\beta  {\left( {{\rho _\beta }{S_\beta }{U_\beta } + \frac{1}{2}{\rho _\beta }{S_\beta }U_\beta ^2} \right)}$$                                                                               (4-39)

where _U_ is the internal energy of phase , and _u_ is the average phase velocity in the wellbore. The two right-hand-side terms in Eq. 4-39 represent the accumulation of internal and kinetic energy, respectively.

_**Flow Terms**_

Transport along the wellbore is governed in general by processes of advection, diffusion, and dispersion, and is also subject to other processes such as exchanges with the formation at feed zones.  The total advective mass transport term for a component can be written in one-dimension as

$${F^\kappa } = -\frac{1}{A}\left[ {\frac{{\partial ({A\rho _G}X_G^\kappa S_G{u_G})}}{{\partial z}} + \frac{{\partial ({A\rho _L}X_L^\kappa S_L{u_L})}}{{\partial z}}} \right]$$                                                                  (4-40)

where $$u_{\beta}$$ is the average velocity vector of phase within the wellbore, A is the well cross-sectional area, and _z_ is the along-wellbore coordinate (can be vertical or horizontal).

The transport terms for energy in the wellbore include those due to (1) advection, (2) kinetic energy, (3) potential energy, and (4) lateral wellbore heat loss/gain.  The overall one-dimensional energy transport term can be written as

&#x20;$${F^e} = -\lambda \frac{\partial T} {\partial z} -\frac{1}{A}\sum\limits_\beta  {\frac{\partial }{{\partial z}}\left( {{A\rho _\beta }{S_\beta }({u_\beta h_\beta}} +  {\frac{1}{2}{ }u_\beta ^2} \right)- \sum\limits_\beta {(g S_\beta\rho _\beta }{u_\beta } cos\theta)}   - {q^{''}}$$         (4-41)

where $$h_{\beta}$$ is specific enthalpy of fluid phase $$\beta$$ , _g_ is the gravitational acceleration, $$\theta$$is the incline angle of the wellbore, and _q"_ is the wellbore heat loss/gain per unit length of wellbore (optional if the surrounding formation is not explicitly represented in the numerical grid).

Note that the mass or energy exchange terms between a perforated wellbore section and its surrounding formation are omitted from the above equations for simplicity. These terms are calculated as flow through porous media as implemented in normal TOUGH except that the nodal distance to the interface on the wellbore side is set to zero in the grid.

&#x20;_**Momentum Conservation Using the Drift-Flux Model (DFM)**_

In order to model the advective transport terms ( $$F_\beta$$and $$u_\beta$$), we invoke the DFM (Zuber and Findlay, 1965; Shi et al., 2005) to describe both single-phase and multiphase flow in wellbores. The basic idea of the DFM is to consider the two-phase liquid-gas mixture as a single effective fluid phase with slip between gas and liquid arising from non-uniform velocity profiles, as well as from buoyancy forces accounted for by empirically relating phase fractions and velocities to the mixture velocity.

The gas velocity $$u_G$$ is related to the mixture velocity u as follows:&#x20;

$${u_G} = {C_0}u + {u_d}$$                                                                                                              (4-42)&#x20;

where $$C_0$$ is the profile parameter (or distribution coefficient), and $$u_d$$ is the drift velocity of the gas describing the buoyancy effect (Shi et al., 2005),

$${u_d} = \frac{{(1 - {C_0}{S_G}){C_0}{u_C}{K_u}}}{{{C_0}{S_G}\sqrt {\frac{{{\rho _G}}}{{{\rho _L}}}}  + 1 - {C_0}{S_G}}}$$                                                                                                   (4-43)

where $$K_u$$ is the Kutateladze number and $$u_c$$ is the “characteristic velocity,” a measure of the velocity of bubble rise in a liquid column, given by

$${u_C} = {\left[ {\frac{{g{\sigma _{GL}}({\rho _L} - {\rho _G})}}{{{\rho _L}^2}}} \right]^{\frac{1}{4}}}$$                                                                                                       (4-44)&#x20;

where $$\sigma_{GL}$$ is the surface tension between gas and liquid phases. By definition, the average mixture velocity (u) is the volumetrically weighted velocity

$$u = {S_G}{u_G} + (1 - {S_G}){u_L}$$                                                                                                (4-45)

Therefore, the liquid velocity can be determined as

$${u_L} = \left( {\frac{{1 - {S_G}{C_0}}}{{1 - {S_G}}}} \right)u - \left( {\frac{{{S_G}}}{{1 - {S_G}}}} \right){u_d}$$                                                                                      (4-46)

The profile parameter $$C_0$$ varies from 1.0 to 1.2 and is assumed to be a smooth function of gas saturation:

$${C_0} = \left\{ \begin{array}{l} 1.2,{S_G} < {S_1}\\ 1 + 0.1\left[ {1 + \cos \left( {\pi \frac{{{S_G} - {S_1}}}{{{S_2} - {S_1}}}} \right)} \right],{S_1} < {S_G} < {S_2}\\ 1.0,{S_G} > {S_2} \end{array} \right.$$                                            (4-47)&#x20;

with the two turning saturations, S1 and S2, set at 0.8 and 0.9999, respectively.

To calculate the mixture velocity, we use the transient momentum conservation equation with the steady-state assumption about the wall shear stress. Specifically, starting from the transient momentum equation

$$\frac{\partial }{{\partial t}}(\rho u) + \frac{\partial }{{\partial L}}\left( {\rho {u^2}} \right) =  - \frac{{\partial P}}{{\partial L}} - \frac{{f\rho {u^2}}}{{4{r_w}}} - \rho g\cos \theta$$                                                              (4-48)

where u is the mixture velocity in the wellbore, L is a length of the wellbore section (positive upward), ρ is the mixture density and θ is the local angle between wellbore section and the vertical direction. The friction coefficient (f) is a function of the Reynolds number (Re) for laminar and turbulent flows by

$$f = \frac{{64}}{{{\mathop{\rm Re}\nolimits} }}{\rm{ \enspace  for  \enspace Re < 2400 }} \\ \frac{1}{{\sqrt f }} =  - 2\log \left[ {\frac{{2\varepsilon /d}}{{3.7}} - \frac{{5.02}}{{{\mathop{\rm Re}\nolimits} }}\log \left( {\frac{{2\varepsilon /d}}{{3.7}} + \frac{{13}}{{{\mathop{\rm Re}\nolimits} }}} \right)} \right] \enspace  for  \enspace  Re > 2400$$                                  (4-49)

where the Reynolds number is defined as  $$Re=\frac{\rho u d}{\mu}$$, μ is the mixture viscosity.

The fundamental challenge of implementing the transient DFM is the coupling that exists between friction factor and velocity. The first-order approach is to use a velocity from the prior time step to calculate the friction factor for the current time step. Further detailed discussions can be found in Pan et. al. (2010)
