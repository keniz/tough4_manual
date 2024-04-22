# Virtual Node Well Treatment

The well boundary condition can also be treated using a “virtual node” method (Wu et al., 1996; Wu, 1999; Wu, 2000). The method handles a wellbore as a single or several computational nodes screened and connected to many neighboring nodes for a multi-layered well. The wellbore can be vertical, inclined, or horizontal. A borehole node is treated in the same way as for any other non-well nodes, and pumping/injection conditions are accounted for using sink or source terms to the node, depending on whether they are flux-specified or pressure-specified. In general, the mass balance Equations are still applicable to well node _i_. It is assumed in TOUGH4 that a well node is subject only to pumping or injection operations without any other boundary conditions. For simplification, the equations discussed in this section are for three phases (aqueous, gas and oil phases) and each phase with single mass component (water in aqueous, gas in the gas phase, and oil in the oil phase). The only difference for a system with multiple components in each phase is by multiplying the mass fractions ($$X_\beta^\kappa$$) in each phase to the accumulation terms and the flux terms.  Therefore, the equation (5-7) for well node _i_, cab be rewritten in the form:

$$R_i^{\beta ,k + 1} = \left\{ {\left[ {\varphi {S_\beta }{\rho _\beta }} \right]_i^{k + 1} - \left[ {\varphi {S_\beta }{\rho _\beta }} \right]_i^k} \right\}\frac{{{V_i}}}{{\Delta t}} - Q_{\beta ,\beta }^{k + 1} - \sum\nolimits_{j \in {\eta _i}} {\left( {{\rho _\beta }{\lambda _\beta }} \right)_{ij + 1/2}^m} P{I_{ij}}\left[ {\psi _{\beta j}^{k + 1} - \psi _{\beta i}^{k + 1}} \right]$$           (4-25)

where  $$PI_{ij}$$ is a well productivity or injectivity index for connection between well node _i_ and neighboring node _j_; $$Q_{\beta ,\beta}^{n + 1}$$ is the total mass rate ( $$\beta$$ is both phase and component index, = g, w or o) of pumping or injection at the well, to be determined in the following for different pumping or injection specifications; and _j_ is the index of a neighboring formation node, connected to well node _i_.  $$\lambda _\beta$$ is the mobility of fluid in phase $$\beta$$.

It should be pointed out that from now on we will drop the subscript for time level (_k_, _k_+1) in the equations for convenience (for this section only), and always assume that well boundary condition terms are evaluated fully implicitly.

There are many methods and equations, especially in the petroleum industry literature, for evaluating the well index, Typically, equation (4-15) is used for $$PI_{ij}$$ calculation.  The user is recommended to refer to the literature for various well indexes of vertical, inclined or horizontal wells (Peaceman, 1978, 1982, 1991, and 1995; Lee et al., 1993; and Fung et al., 1991).

The injection rate for phase  $$\beta$$ (= g, w or o) at an injection well is evaluated by

$${Q_{\beta ,\,\beta}} = \sum\limits_{j\, \in \,{\eta _i}} {\left( {{\rho _\beta }\,{\lambda _\beta }} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}\left[ {{P_{\beta ,\,j}} - {P_w} - {\rho _\beta }\,g\;\left( {{D_j} - {D_w}} \right)} \right]$$                                                            (4-26)

In above equation, the total mass rate is calculated from summation of the flow terms between well node, _i_, and all its neighbors of formation nodes, _j_;  $$P_w$$ is the well pressure, determined using an additional constraint equation in the following discussions; $$D_w$$is the depth at which a pump of pumping or injection is located inside the wellbore; $$D_j$$is the depth of node j. It is important to note that the Z coordinate of the well elements and elements connected to them must be provided for the calculation $$D_w$$and $$D_j$$, which are not required by original TOUGH simulation.&#x20;

The mobility terms ( $$\lambda$$) in the well flow Equations of (4-26) are evaluated using the upstream weighting schemes.  In other words, the well node is treated as a virtual node, like any other node in the grid, except that the sink/source term is determined by Equations (4-26).  The following subsections will provide detailed treatment for different pumping and injection scenarios.&#x20;

In applying the “virtual ‘node” method, special attention is needed to specifying the “rock properties” to the virtual node.  Capillary pressure and relative permeability functions are also needed for all the well nodes, and should be specified differently for a particular phase, depending on if it is at a pumping or injection condition.  All the flow properties and constitutive correlations are needed for well nodes, since the well node is regarded as a normal grid block in the solution.

**Rate-Specified Pumping Well**

There are in general two types of rate-specified pumping wells: (a) total liquid (water and oil) volumetric pumping rate is specified, and (b) one-phase liquid pumping volumetric rate is specified, including oil, gas or water pumping rate. The two rate-specified pumping scenarios are treated differently in this section. The following approach is not only rigorous and efficient in treating a pumping well, but also allows back flow to occur. The back flow may occur at certain layers in a thick-screened, pumping well, which penetrates multi-layers, or along a long horizontal well, which cannot be controlled in general in the ground, and needs to be determined by the code.

_Total Liquid Rate Specification_

With a total volumetric pumping rate, $$Q_L$$ (> 0), of liquid (water + oil) is specified at the well, the well flowing pressure is evaluated by,

$${P_{\,w}} = \left\{ { - {Q_L} + \sum\limits_{j\, \in \,{\eta _i}} {\sum\limits_\beta  {\left( {{\rho _\beta }\,{\lambda _\beta }/\rho _\beta ^o} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}\left[ {{P_{\beta ,\,j}} - {\rho _\beta }\,g\;\left( {{D_j} - {D_w}} \right)} \right]} } \right\}\\ \quad \quad  \div \left\{ {\sum\limits_{j\, \in \,{\eta _i}} {\sum\limits_\beta  {\left( {{\rho _\beta }\,{\lambda _\beta }/\rho _\beta ^o} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}} } \right\}$$                                   (4-27)

with $$\beta$$ = o and w.

The well pressure determined by Equation (4-27) is subject to a constraint,

$${P_{\,w}} \ge {P_{w,\,\min }}$$                                                                                                                                             (4-28)

where  $$P_{w,min}$$ is the minimum well pressure allowed.  Using Equation (4-28) is to enforce a physical constraint that it is not always possible to produce liquid at the specified rate.  If not, the pumping well is switched to a pressure-specified pumping operation.

The actual pumping rate, to be added to Equations (4-25) as a sink term, is evaluated using Equation (4-26) for different mass components, respectively, with the well pressure determined by Equation (4-27).  In addition, gas phase is also flowing out simultaneously at the well, which we have no control on, even though a liquid rate is specified.  In general, the well pressure, $$P_w$$  from (4-27) and (4-28), should approach the well nodal pressure, $$P_i$$, from the simulation when a solution is converged and if zero capillary forces are specified for the well node.

_Single-Phase Rate Specification_

&#x20;With a single-phase liquid volumetric pumping rate, $$Q_\beta( > 0 )$$, of oil, water or gas, is specified at the well, the well pressure is evaluated as follows,

$${P_{\,w}} = \left\{ { - \rho _{\beta ,{\kern 1pt} STC}^{}{Q_o} + \sum\limits_{j\, \in \,{\eta _i}} {\left( {{\rho _\beta }\,{\lambda _\beta }} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}\left[ {{P_{\beta ,\,j}} - {\rho _\beta }\,g\;\left( {{D_j} - {D_w}} \right)} \right]} \right\} \\ \quad \quad \div \left\{ {\sum\limits_{j\, \in \,{\eta _i}} {\left( {{\rho _\beta }\,{\lambda _o}} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}} \right\}$$                                    (4-29)

with $$\beta=o,w,\quad or \quad g$$, where $$\rho_{\beta,STC}$$ is the density of phase $$\beta$$ at standard conditions.

The well pressure from (4-29) is also subject to a constraint condition (4-28) physically. Then the actual pumping rate for the phase is evaluated using Equations (4.3.6) to (4.3.8) and added to Equations (4.3.1) to (4.3.3).  Again non-specified phases may be pumped out, and their flow terms should also be accordingly calculated subject to the same well pressure.

**Pressure-Specified Pumping Well**

If a pumping well is operated at a specified well pressure, this pressure is directly substituted into Equations (4.3.1) to (4.3.3) for Pw. This type of pumping condition is generally named as production under “deliverability”. In this case, any phase or all of the three phases may be produced, which are decided by the formation conditions at the nodes connected to the well. In TOUGH4, three sink terms for the three phases are calculated using (4-26), respectively, and then added to Equations (4-25).

Rate-Specified Injection Well

For injection wells, injection rates are known in practice. The injected phase can be water, oil (maybe), and gas. In this case, back flow (i.e., pumping a phase from the well) is not allowed. With a total mass injection rate, $$Q_{\beta}( > 0)$$,  of phase $$\beta$$, specified at the well, the well injection pressure is then evaluated by,

$${P_{\,w}} = \left\{ {{Q_\beta } + \sum\limits_{j\, \in \,{\eta _i}} {\left( {{\rho _\beta }\,{\lambda _\beta }} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}\left[ {{P_{\beta ,\,j}} - {\rho _\beta }\,g\;\left( {{D_j} - {D_w}} \right)} \right]} \right\} \\ \quad \div \left\{ {\sum\limits_{j\, \in \,{\eta _i}} {\left( {{\rho _\beta }\,{\lambda _\beta }} \right)_{i\,j + 1/2}^{}} P{I_{i\,j}}} \right\}$$                                                     (4-30)

with $$\beta = o,\quad  w \quad or \quad g$$, and the well injection pressure is subject to the following constraint,

$${P_{\,w}} \le {P_{w,\,\max }}$$                                                                            &#x20;

where $$P_{w,max}$$ is the maximum well injection pressure allowed.  Equation (4.3.13) is used for the situation that the specified injection rate may be too high for the well condition, and then the injection well is switched to a pressure-specified injection operation.

The actual injection rate for the specified phase is evaluated using Equation (4.3,5),  with the well injection pressure determined by Equations (4.3.12) and (4.3.13), and then is added to Equations (4.3.1) and (4.3.3) for well node i.

Pressure-Specified Injection Well

If a fluid is injected at a specified well pressure, this pressure is directly substituted into Equation (4.3.5) for $$P_w$$  for the injected phase. This type of injection condition can be treated using the big-volume method, as discussed in Section 4.1, if it is a single grid layer injection well. However, for a multi-layered injection well, the injection rate of the specified phase must be determined and partitioned using Equation (4.3.5), and then added to (4.3.1), (4.3.2), or (4.3.3), accordingly.

Special Considerations for Treatment of Well Conditions

The virtual node approach for treating well conditions, as discussed above, is a general, flexible and efficient method.  The major advantages of the virtual node scheme, as compared with the conventional potential or mobility allocation method, are that it is natural to include “back flow” occurring and to incorporate contributions from all the connections to a well into the Jacobian matrix.  The full Jacobian matrix and the full implicit scheme make the method very robust and stable in solving a multi-layered well flow problem.&#x20;

One potential problem, however, is that since the wellbore node has a very small volume and high flow rates, it may cause some numerical difficulty during a Newton iteration.  This problem can be alleviated by increasing the volume of the wellbore nodes by a factor of 102 - 103.  This has the effect of adding a pseudo wellbore storage effect and dampens out oscillations in the Newton iteration (Wu et al., 1996).  Unless one is interested in very small-scale transient behavior of wells, numerical tests indicate that this pseudo wellbore storage has almost no effects on the converged solution.  It is recommended that the pseudo wellbore storage approach should be always used for rate-specified pumping or injection problems.  For pressure-specified pumping or injection problems, however, an infinite-large volume of a wellbore can also be used to obtain a much better numerical performance.
