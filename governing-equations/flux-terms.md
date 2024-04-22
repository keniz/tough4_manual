# Flux Terms

Advective mass flux is a sum of phase fluxes,

$$\left.\ \mathbf{F}^\kappa\right|_{adv}=\sum_{\beta}{X_\beta^\kappa\mathbf{F}_\beta}$$                                                                        (4-4)

&#x20; where individual phase fluxes are given by a multiphase version of Darcy's law:

$$\mathbf{F}_\beta\quad=\quad\rho_\beta\mathbf{u}_\beta\quad=\quad-\;\ k\;\frac{k_{r\beta}\rho_\beta}{\mu_\beta}\;(\nabla\ P_\beta-\;\rho_\beta g)$$                      (4-5)

&#x20;  where, $$u_\beta$$ is the Darcy velocity (volume flux) of phase $$\beta$$_, k_ is absolute permeability, $$k_{r\beta}$$ is relative permeability to phase $$\beta$$_,_ $$\mu_\beta$$ is the phase dynamic viscosity, and

$$P_\beta=\ P+\ P_{c\beta}$$

is the fluid pressure in phase $$\beta$$, which is the sum of the pressure _P_ of a reference phase (usually taken to be the gas phase) and the capillary pressure $$P_{c\beta}(\le0)$$.  g is the vector of gravitational acceleration. Vapor pressure lowering due to capillary and phase adsorption effects can be considered, and is modeled by Kelvin’s equation (Edlefsen and Anderson, 1943),

$$P_v\left(T,S_l\right)=\ f_{VPL}\left(T,S_l\right)\cdot\ P_{sat}\left(T\right)$$                                             (4-6)

&#x20; where

$$f_{VPL}=\ ex p{\left[\frac{M_w\; P_{cl}\left(S_l\right)}{\rho_lR\left(T+273.15\right)}\right]}$$                                                              (4-7)

is the vapor pressure lowering factor. $$P_v$$is the vapor pressure, $$P_{sat}$$is the saturated vapor pressure of bulk aqueous phase, $$P_{cl}$$is the capillary pressure (i.e., the difference between aqueous and gas phase pressures), $$M_w$$ is the molecular weight of water, and _R_ is the universal gas constant.

Absolute permeability of the gas phase increases at low pressures according to the relation given by Klinkenberg (1941)

$$k=\ k_\infty\left(1\;+\;\frac{b}{P}\right)$$                                                                             (4-8)&#x20;

where $$k_∞$$is the permeability at “infinite” pressure, and _b_ is the Klinkenberg parameter.

In addition to Darcy flow, mass transport can also occur by diffusion. Diffusive flux is modeled as follows:

$$\mathbf{f}_\beta^\kappa=-\varphi\tau_0\tau_\beta\rho_\beta d_\beta^\kappa\nabla\ X_\beta^\kappa$$                                                                    (4-9)

where $$d_\beta^\kappa$$ is the molecular diffusion coefficient for component _k_ in phase $$\beta$$, and $$\tau_0 \tau_\beta$$ is the tortuosity, which includes a porous medium dependent factor $$\tau_0$$ and a coefficient that depends on phase saturation $$S_\beta$$ _,_ $$\tau_\beta=\tau_\beta(S_\beta)$$. For general two-phase conditions, the total diffusive flux is then given by

$$f^\kappa \quad=\quad-\Sigma_l^\kappa\nabla\ X_l^\kappa\;-\;\Sigma_g^\kappa\nabla\ X_g^\kappa$$                                                  (4-10)

where $$\Sigma_\beta^\kappa=\varphi\tau_0\tau_\beta\rho_\beta d_\beta^\kappa$$ is an effective diffusion coefficient in phase $$\beta$$. We have used this pragmatic approach because it is not possible to formulate a model for multiphase diffusion that would be accurate under all circumstances. The basic Fick law works well for diffusion of tracer solutes that are present at low concentrations in a single-phase aqueous solution at rest with respect to the porous medium $$^{[1]}$$.

Several models are available to describe the dependence of tortuosity on porous medium properties and phase saturation. For the relative permeability model, tortuosity will be taken as $$\tau_0 \tau_\beta(S_\beta)=\tau_0k_{r\beta}(S_\beta)$$with the user-specified porous medium dependent factor $$\tau_0$$. The Millington and Quirk (1961) model, which has frequently been used for soils (Jury et al., 1983; Falta et al., 1989), yields non-zero tortuosity coefficients as long as phase saturation is non-zero $$^{[2]}$$.

$$\tau_0\tau_\beta=\varphi^\frac{1}{3}\;{S_\beta}^\frac{10}{3}$$                                                                                    (4-11)\
For the constant diffusivity formulation, $$\tau_0 \tau_\beta=S_\beta$$ will be used. This alternative corresponds to the formulation for gas diffusion in the original version of TOUGH2. In the absence of phase partitioning and adsorptive effects, it amounts to effective diffusivity being approximately equal to $$d_\beta^\kappa$$, independent of saturation. This can be seen by noting that the accumulation term in the phase $$\beta$$contribution to the mass balance equation for component _k_ is given by $$\varphi\ S_\beta\rho_\beta X_\beta^\kappa$$, approximately canceling out the $$\varphi\ S_\beta\rho_\beta$$ coefficient in the diffusive flux.

TOUGH4 can model the pressure and temperature dependence of gas phase diffusion coefficients by the following equation (Vargaftik, 1975; Walker et al., 1981).

$$d_g^\kappa(P,T)=\ d_g^\kappa(P_0,T_0)\;\frac{P_0}{P}\;\left[\frac{T+273.15}{273.15}\right]^\theta$$                                            (4-12)

At standard conditions of $$P_0$$ = 1 atm = 1.01325 bar and $$T_0$$ = 0˚C, the diffusion coefficient for vapor-air mixtures has a value of $$2.13 \times10 ^{-5}m^2/s$$; parameter $$\theta$$for the temperature dependence is 1.80. Presently there are no provisions for inputting different values for the parameter $$\theta$$ of temperature dependence for different gas phase components. Diffusion coefficients for the non-gaseous phases are taken as constants, with no provisions for temperature dependence of these parameters.

Heat flux includes conductive, convective, and radiative components:

$$\mathbf{F}^h=-\lambda\nabla\ T\;+\;\sum_{\beta}{h_\beta\mathbf{F}_\beta}+f_\sigma\sigma_0\nabla\ T^4$$                                      (4-13)  &#x20;

where $$\lambda$$ is the effective thermal conductivity, and $$h_\beta$$ is the specific enthalpy in phase $$\beta$$,  $$f_\sigma$$is the radiant emittance factor, and $$\sigma_0$$ is the Stefan-Boltzmann constant.

***

\[1] Many subtleties and complications can arise when multiple components diffuse in a multiphase flow system. Effective diffusivities in general may depend on all concentration variables, leading to nonlinear behavior especially when some components are present in significant (non-tracer) concentrations. Additional nonlinear effects arise from the dependence of tortuosity on phase saturations, and from coupling between advective and diffusive transport. For gases, the Fickian model has serious limitations even at low concentrations, which prompted the development of the “dusty gas” model that entails a strong coupling between advective and diffusive transport (Mason and Malinauskas, 1983; Webb, 1998) and accounts for molecular streaming effects (Knudsen diffusion) that become very important when the mean free path of gas molecules is comparable to pore sizes. Further complications arise for components that are both soluble and volatile, in which case diffusion in aqueous and gaseous phases may be strongly coupled via phase partitioning effects. An extreme case is the well-known enhancement of vapor diffusion in partially saturated media, which is attributed to pore-level phase change effects (Cass et al., 1984; Webb and Ho, 1998a, b). These alternative models are not implemented in TOUGH4.

\[2] It stands to reason that diffusive flux should vanish when a phase becomes discontinuous at low saturations, suggesting that saturation-dependent tortuosity should be related to relative permeability, i.e., $$\tau_\beta(S_\beta) \approx k_{r\beta}(S_\beta)$$_._ However, for components that partition between liquid and gas phases, a more complex behavior may be expected. For example, consider the case of a volatile and water-soluble compound diffusing under conditions of low gas saturation where the gas phase is discontinuous. In this case we have $$k_{rg}(S_g)=0$$ (because $$S_g \lt S_{gr}$$), and $$k_{rl}(S_l=1-S_g) \lt 1$$, so that a model equating saturation-dependent tortuosity to relative permeability would predict weaker diffusion than in single-phase liquid conditions. For compounds with “significant” volatility this would be unrealistic, as diffusion through isolated gas pockets would tend to enhance overall diffusion relative to single-phase liquid conditions.
