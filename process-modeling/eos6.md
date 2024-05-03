# EOS6

1. **Description**&#x20;

EOS6, was developed for simulation of one or two-phase non-isotheral flow of a single gas and water mixture in subsurface. The gas can be any gas listed in the  [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/fluid/). In general, EOS6 is used for simulation of a gas that is not covered by other EOS modules, such as the noble gases. Thermophysical properties of the gas are directly read and interpolated from the database by NIST Chemistry WebBook. Gas solubility, which has not been provided by NIST database, is determined using the Herry’s Law or user defined model.  All water properties are represented by the steam table equations as given by the International Formulation Committee (1967). The selected gas is approximated as an ideal gas, and additivity is assumed for the gas and vapor partial pressures in the gas phase, _Pg = Pa + Pv,_ where _Pa_ is the partial pressure of the gas component. The gas phase viscosity and enthalpy are calculated using molar fraction weighted arithmetic mean of the gas component and vapor. The impact of dissolved gas on density, viscosity and enthalpy of the aqueous phase is neglected.&#x20;

Solubility of gas in liquid water is represented by Henry's law (see Eq. 7-2). TOUGH4 provides three methods for calculation of Henry’s constant:

(1) Read the table of temperature dependent Henry’s constants from a user provided data file. The Henry’s constant at a given temperature is calculated by interpolation of the table.

(2) Use equation (Cramer,1982):

$$K_h=\dfrac{1}{(b_1+b_2T+b_3T^2+b_4T^3+b_5T^4+b_6T^5+b_7T^6+b_8T^7)*101325.0}$$               (7-5)

(3) Use equation (Damore and Truesdell, 1988):

$$K_h=10.0^{-6}e^{-(b_1+b_2/T+b_3*log(T))}$$                                                                                             (7-6)

For input of the constant parameters ($$b_1, b_2, ....., b_8$$), user may refer to the keyword "[GASES](../preparation-of-model-input/keywords-and-input-data/gases.md)", record _**GASES.2**_**.**&#x20;

2. **Specifications**

A summary of EOS6 specifications and parameters is given in Table 9. The default number of mass components is 2 and maximum number is 7. Simulation can be run in isothermal or non-isothermal. The set of primary thermodynamic variables is (P, Xg, T) for single-phase, (Pg, Sg + 10, T) for two-phase conditions. Use of Sg+10 as primary variable is for distinguishing the phase condition based on value range of the second primary variable. &#x20;

Table 9 Summary for EOS6

<table><thead><tr><th width="295">Specification</th><th>Parameters</th></tr></thead><tbody><tr><td>Components</td><td><p>(1) Water</p><p>(2) Gas (user specified gas)</p><p>(3-7) Tracer1-Tracer5 (optional)</p></td></tr><tr><td>Phase condition and its state name and index</td><td><p>(1) Gas, GAS </p><p>(2) Aqueous, AQU </p><p>(3) two-phase, AQG</p></td></tr><tr><td>Primary variables</td><td>See <a href="../preparation-of-model-input/inputs-for-initial-conditions/eos6.md">Table 23</a></td></tr><tr><td>Optional process modeling</td><td>Molecular diffusion, Vapor pressure Lowering, Wellbore simulation, Biodegradation reactions, and non-isothermal simulation. </td></tr></tbody></table>



3. **Specific input requirements**

EOS6 simulation requires definition of the gas component through input keyword "[GASES](../preparation-of-model-input/keywords-and-input-data/gases.md)" and accesses the database of selected gas thermophysical properties (gas\_properties.dat). The file "gas\_properties.dat" must be copied into the working folder where the model input files are located. This file may be obtained from someone who had done the simulation for the same gas component, or users can create their own database by following steps:

(1). Go to  [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/fluid/) website.&#x20;

(2). Use the pull-down menu (item 1) to select the gas species; choose the units that are used in TOUGH4 simulation (see Figure 16).

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption><p>Figure 16. Interface for download the gas thermophysical properties and selection of the units</p></figcaption></figure>

(3). Decide the range of temperature and pressure to be included in database of the gas properties (see Figure 17）. The range must fully cover the pressure and temperature of the models that you are going to run. The gas properties to be downloaded is for a constant temperature at each time. The pressure increment must be reasonable. If it is too large, the interpolation results may have bad accuracy. If it is too small, the data file will be very large and the interpolation will be less efficient. Several hundred points may be appropriate for each temperature.  Download the lowest temperature first.&#x20;

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption><p>Figure 17. Define temperature and pressure range for gas thermophysical property data download</p></figcaption></figure>

(4). Download the data file as a tab-delimited text file (see Figure 18). The data file may be named as "5.dat" for the file at temperature 5 $$^oC$$. The pressure increment can be different at different pressure ranges. This can be done by downloading multiple times for the same temperature, each time covering a different range of pressure with different increment. Combine the multiple downloaded files into a single file in the sequence of increasing pressure. The first two lines (headers and units) in the downloaded files must be deleted except the first file.&#x20;

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption><p>Figure 18. Thermophysical property data for the selected gas at given temperature </p></figcaption></figure>

(5). Repeat step (3) and (4) to download the data file for different temperatures, e.g. for temperature=8, 11, 14, ...., 150 $$^oC$$, get files 8.dat, 11.dat, 14.dat, ......, 150.dat. The increment of temperature can be different. Combine the downloaded files into a single file "gas\_properties.dat" in the sequence of increasing temperature.  The first two lines (headers and units) in the downloaded files must be deleted except the first file.

The format of the file "gas\_properties.dat" is ready to be read by TOUGH4. Users can use this file directly in the EOS6 simulations. You are welcome to share the "gas\_properties.dat" with other EOS6 users.

Gas properties from other sources are also allowed. It is required to include at least the 5 essential columns (temperature, pressure, density, enthalpy, viscosity). The data file must use the same headers and units as the downloaded NIST data file and all data are separated by spaces. &#x20;
