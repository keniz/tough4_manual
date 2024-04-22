# Sink and Source Terms

Sinks and sources are introduced by specifying the mass production (_q_ < 0) or injection (_q_ > 0) rates of fluids as well as heat flow. Any of the mass components may be injected in an element at a constant or time-dependent mass rate, and the specific enthalpy of the injected fluid may be specified as well. Heat sources/sinks (with no mass injection) may be either constant or time dependent.

In the case of fluid production, a total mass production rate needs to be specified. The phase composition of the produced fluid may be determined by the relative phase mobilities in the source element. Alternatively, the produced phase composition may be specified to be the same as the phase composition in the producing element. In either case, the mass fractions of the components in the produced phases are determined by the corresponding component mass fractions in the producing element.

TOUGH4 also includes different options for considering wellbore flow effects: a well on deliverability against specified bottomhole or wellhead pressure, or coupled wellbore flow.  Details are discussed below.

_**Deliverability Model**_

Production wells may operate on deliverability against a prescribed flowing bottomhole pressure, $$P_{wb}$$, with a productivity index PI (Coats, 1977). With this option, the mass production rate of phase $$\beta$$ from a grid block with phase pressure $$P_\beta \gt P_{wb}$$_Pb_ is

$$q_\beta=\frac{k_{r\beta}}{\mu_\beta}\;\rho_\beta\cdot\ PI\cdot(P_\beta-P_{wb})$$                                                                 (4-14)

&#x20;For steady radial flow, the productivity index of layer _l_ is given by (Coats, 1977; Thomas, 1982)

&#x20; $$(\mathrm{\mathrm{PI}})_l=\frac{2\pi\left(k\Delta z_l\right)}{ln{\left(\frac{r_e}{r_w}\right)}\;+s\;\;-\;\frac{1}{2}}$$                                                                               (4-15)                                                                         &#x20;

where, $$\Delta\ z_l$$ denotes the layer thickness, $$(k\Delta\ z_l)$$ is the permeability-thickness product in layer _l_, $$r_e$$is the grid block radius, $$r_w$$ is the well radius, and _s_ is the skin factor. If the well is producing from a grid block which does not have cylindrical shape, an approximate PI can be computed by using an effective radius

&#x20;$$r_e=\sqrt{\frac{A}{\pi}}$$                                                                                                    (4-16)

where _A_ is the grid block area; e.g., _A =_ $$\varDelta$$_x •_ $$\varDelta$$_y_ for an areal Cartesian grid. More accurate expressions for specific well patterns and grid block shapes have been given in the literature (e.g., Peaceman, 1977, 1982; Coats and Ramesh, 1982).

The rate of production for mass component _k_ is

$${\hat{q}}^\kappa=\sum_{\beta}{\; X_\beta^\kappa\;}q_\beta$$                                                                                        (4-17)

For wells that are screened in more than one layer (element), the flowing wellbore pressure $$P_{wb}$$can be corrected to approximately account for gravity effects according to the depth-dependent flowing density in the wellbore. Assume that the open interval extends from layer _l_ = 1 at the bottom to _l_ = _L_ at the top. The flowing wellbore pressure in layer _l_, $$P_{wb,l}$$, is obtained from the wellbore pressure in layer _l_ + 1 immediately above it by means of the following recursion formula

$$P_{wb,l}=P_{wb,l+1}+\frac{g}{2}\left(\rho_l^f\Delta z_l+\rho_{l+1}^f\Delta z_{l+1}\right)$$                                            (4-18)

Here, _g_ is acceleration of gravity, and $$\rho_l^f$$ is the flowing density in the tubing opposite layer _l._ Flowing densities are computed using a procedure given by Coats (private communication, 1982). If wellbore pressure were zero, we would obtain the following volumetric production rate of phase $$\beta$$ from layer _l._

$$r_{l,\beta}=\left(\frac{k_{r\beta}}{\mu_\beta}\right)_l(\mathrm{\mathrm{PI}})_l\; P_{l,\beta}$$                                                                              (4-19)

The total volumetric flow rate of phase $$\beta$$ opposite layer _l_ is, for zero wellbore pressure

$$r_{l,\beta}^T=\displaystyle\sum_{m=1}^{l}r_{m\beta}$$                                                                                             (4-20)

From this, we obtain an approximate expression for flowing density opposite layer l which can be used in Eq. (4-18).

$$\rho_l^f=\frac{\sum_{\beta}{\rho_{l,\beta}r_{l,\beta}^T}}{\sum_{\beta}\ r_{l,\beta}^T}$$                                                                                              (4-21)      &#x20;

During fluid production or injection, the rate of heat removal or injection is determined by

$${\hat{q}}^h=\sum_{\beta}{\; q_\beta\; h_\beta}$$                                                                                            (4-22)

where $$h_b$$ is the specific enthalpy of phase $$\beta$$.

_**Coupled Wellbore Flow**_

Production wells typically operate at (nearly) constant wellhead pressures. However, as flow rate and flowing enthalpy change with time, wellbore pressure gradients and flowing bottomhole pressures will also change. TOUGH4 can directly describe production from wells by solving equations for flow in the reservoir and flow in the wellbore in a fully coupled manner (see the Section [Drift Model](drift-model.md)). TOUGH4 can also use an alternative approach (Murray and Gunn, 1993) in which the wellbore and reservoir simulations are performed separately. This can be accomplished by running a wellbore flow simulator prior to the reservoir simulation for a range of flow rates _q_ and flowing enthalpies _h_ in order to generate a table of flowing bottomhole pressures $$P_{wb}$$_._\
$$P_{wb}=P_{wb}\left(q,h;P_{wh},z,r_w\right)$$                                                                        (4-23)

In addition to the functional dependence on _q_ and _h,_ flowing bottomhole pressure is dependent on a number of well parameters. These include wellhead pressure $$P_{wh}$$, feed zone depth _z_, wellbore radius $$r_w$$, friction factors, and possibly others. By interpolating on these tabular data, the above equation can be directly inserted into the well source term. Reservoir flow equations that include a quasi-steady approximation to wellbore flow can then be solved with little added computational expense compared to the case where no wellbore flow effects are considered. Advantages of representing wellbore flow effects through tabular data include increased robustness and computational efficiency. It also makes it possible to use different wellbore simulators and two-phase flow correlations without any programming changes in the reservoir simulation code.

We have incorporated a tabular interpolation scheme for dynamic changes of flowing bottomhole pressure into TOUGH4. Flowing enthalpy at the feed zone is known from phase mobilities and enthalpies calculated by the reservoir simulator. The unknown well flow rate and flowing bottomhole pressure are obtained by Newton-Raphson iteration on

$$R(q)\equiv\ q-\;\left(\sum{\frac{k_{r\beta}}{\mu_\beta}\;\rho_\beta}\right)\cdot\ PI\cdot\left(P-P_{wb}(q,h)\right)=0$$                           (4-24)&#x20;

The iterative solution of this equation was embedded in the outer (Newtonian) iteration performed by TOUGH4 on the coupled mass and heat balance equations. Additional computational work in comparison to conventional simulations with constant downhole pressure is insignificant.

The approach is limited to wells with a single feed zone and can only handle wellbore pressure effects from changing flow rates and enthalpies. Effects from changing fluid composition, as, e.g., variable non-condensible gas content, are not modeled at present.
