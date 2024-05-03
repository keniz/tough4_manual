# EOS2

1. **Description**&#x20;

This fluid property module originally was developed by O'Sullivan et al. (1985) for describing fluids in gas-rich geothermal reservoirs, which may contain CO2 mass fractions ranging from a few percent to occasionally 80% or more (Atkinson et al., 1980). EOS2 accounts for non-ideal behavior of gaseous CO2, and dissolution of CO2 in the aqueous phase with heat of solution effects. According to Henry's law, the partial pressure of a non-condensible gas (NCG) in the gas phase is proportional to the mole fraction $$x^{NCG}_{aq}$$ of dissolved NCG in the aqueous phase,

&#x20;          $$P_{NCG}=K_hx^{NCG}_{aq}$$                                                                                                         (7-1)

The Henry’s law coefficient $$K_h$$ for dissolution of CO2 in water is strongly dependent on temperature. The correlation used in the previous release of EOS2 had been developed by O’Sullivan et al. (1985) for the elevated temperature conditions encountered in geothermal reservoirs. It is accurate to within a few percent of experimental data in the temperature range of 40 ˚C ≤ _T_ ≤ 330 ˚C, but becomes rather inaccurate at lower temperatures and even goes to negative values for _T_ < 30 ˚C (see Figure 15). Since TOUGH3, the Henry’s law coefficient calculation was updated with the correlation developed by Battistelli et al. (1997), which is accurate for 0 ˚C ≤ _T_ ≤ 350 ˚C. The Battistelli et al. formulation agrees well with another correlation that was developed by S. White (1996, private communication).

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption><p>Figure 15.  Henry’s law coefficients for dissolution of CO2 in water.</p></figcaption></figure>

The viscosity of vapor - CO2 mixtures is described with a formulation due to Pritchett et al. (1981); other thermophysical property correlations are based on the model of Sutton and McNabb (1977).

2. **Specifications**

A summary of EOS2 specifications is given in Table 6. A more detailed description and application to geothermal reservoir problems are given in the paper by O'Sullivan et al. (1985). The default component number is 2 (water and CO2). Users have the options to include as many as 5 tracers with a maximum component number of 7.&#x20;

&#x20;Table 6 Summary for EOS2

<table><thead><tr><th width="255">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) CO2</p><p>(3-7) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) two-phase, AQG</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eos2.md">Table 20</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation.</td></tr></tbody></table>

