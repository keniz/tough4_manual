# Tracers/Decay Chain

1. **Description**&#x20;

TOUGH4 allows flexibility including as many as 5 tracers or radionuclides in the simulation of any EOS modules. The tracers/radionuclides are treated in different ways for some EOS modules. In general, it is assumed that the phase fluid properties are independent of tracers/radionuclide concentrations (except EWASG).  Implicit in this approximation is the assumption that tracer concentrations are small. Users need to keep this limitation in mind, because TOUGH4 does not provide any intrinsic constraints on tracer concentrations.&#x20;

The tracer components can undergo decay with user-specified half-life, and with radionuclides allowing complex “parent” and “daughter” relations.  Each radionuclide may have multiple "daughters" or/and multiple "parents". The tracers can exist in any user-specified fluid phase, but are not allowed to form a separate non-aqueous fluid phase. Sorption onto the solid grains is also allowed. The decaying components are normally referred to as radionuclides, but they may in fact be any trace components that decay, adsorb, and volatilize (volatilization is included in EOS7 only).  The decay process need not to be radioactive decay, but could be any process that follows a first-order decay law, such as degradation. Stable trace components, such as volatile and water-soluble organic chemicals (VOCs), can be modeled simply by setting half-life to very large values. Simulation of radionuclide decay-chain in TOUGH4 is modified from [EOS7R](https://tough.lbl.gov/assets/docs/TOUGH2\_EOS7R\_Users\_Guide.pdf).  A detailed description of the decay-chain mathematical model and numerical implementation used in EOS7R is available in a laboratory report, which also presents a number of illustrative problems, including verification against analytical solutions (Oldenburg and Pruess, 1995). The decay-chain models can be written as:

$$\dfrac{dM^k}{dt}=-\lambda_k M^k+\alpha_{k-1}\lambda_{k-1} M^{k-1}$$                                                                    (7-30)

where $$M^k$$is the mass of radionuclide _k_ per unit volume, and the decay constant $$\lambda_k$$of radionuclide _k_ is related to the half-life by

$$T_{1/2}=\dfrac{ln 2}{\lambda_k}$$                                                                                                               (7-31)

Radionuclide _k-1_ is the "parent" of radionuclide _k._ $$\alpha_{k-1}$$is the fraction of radionuclide _k-1_ turning into "daughter" _k._ The equation (7-30) allows including multiple "parents" by adding contributions from other "parents" to the right-hand side of the equation. These types of relations are popular in VOC degradation processes, such as the TCE degradation (Figure 23) in which TCE has three "daughter" species, and VC has three "parent" species。&#x20;

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption><p>Figure 24. TCE degradation pathway</p></figcaption></figure>

Adsorption of tracers/radionuclides on the solid grains is modeled as reversible instantaneous linear sorption, so that mass of tracer component _k_ per unit reservoir volume is given by

$$M^k=\varphi\sum_{\beta}{S_\beta\rho_\beta X_\beta^k}+(1-\varphi)\rho_R\rho_{aq}X_{aq}^k K_d$$                                                  (7-32)

where $$K_d$$is the aqueous phase distribution coefficient (de Marsily, 1986, p. 256).

In TOUGH4, tracers may be treated in slightly different way in different EOS modules:

(1) In EOS1. EOS2, EOS3, EOS4, EOS6, and ECO2, tracers can only exist in the user specified phase. If the phase disappears, the tracers are all absorbed to rock grain and will not be accounted in the model any more. Users may need to be careful in defining the tracers and avoid defining the tracers in a phase it may disappear.&#x20;

(2) In EOS7, tracers are allowed in both gas and aqueous phases.  partition between aqueous and gaseous phases according to Henry’s law:

&#x20;$$P_a^k=\ K_h^k x_{aq}^k$$                                                                                                        (7-33)

where $$P_a^k$$ is the partial pressure in the gas phase of tracer _k_, $$K_h^k$$ is Henry’s constant and $$x_{aq}^k$$is the mole fraction of tracer _k_ in the aqueous phase. In EOS7, no solubility constraints are enforced for the brine. Users need to be aware that there are inherent limitations in the ability of a water-brine mixture model to describe processes that involve significant vaporization. Unphysical results may be obtained in thermal problems with strong vaporization effects.

EOS7 uses cubic equation of state to solve thermophysical properties of the gas phase. The tracer contributions to the gas density are added using the ideal gas law. The impact of tracers on the gas viscosity and enthalpy is neglected.  There is no restriction to “small” tracer concentrations in the gas phase, fully allowing gas phase tracer partial pressures.&#x20;

(3) In EWASG, tracers, which are treated as salts, are allowed to exist in both aqueous and solid phase, but not in gas phase. The Solubility model of NaCl remains the same as originally implemented in TOUGH2/EWASG. For other salts, we use a very simple approach as discussed in the [previous section](ewasg.md). &#x20;

(4) In TMVOC and EOS9, tracers are allowed only in aqueous phase.  Tracers in other phases will be neglected.&#x20;

2. **Input requirements**

The tracers can be defined in keyword "[TRACR](../preparation-of-model-input/keywords-and-input-data/tracr.md)" (or "SALTS"). User can input all the required parameters for a tracer through this keyword, no matter whether it is a tracer, radionuclide, solvent, or a salt.  If no tracer is considered in a model, the user just simply neglects the input of this keyword.&#x20;
