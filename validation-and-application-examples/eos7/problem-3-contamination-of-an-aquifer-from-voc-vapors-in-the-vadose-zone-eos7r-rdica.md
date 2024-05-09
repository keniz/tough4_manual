# Problem 3-Contamination of an Aquifer from VOC Vapors in the Vadose Zone (EOS7R/rdica)

This problem is from TOUGH3/EOS7R for simulating the diffusive and advective spreading of volatile organic contaminants (VOCs) in the vadose zone, and their migration across the capillary fringe region into an underlying aquifer.  Figure 10-4 shows the simple model system used in this example, which is an one-dimensional vertical column of 15 m height and 1 $$m^2$$ cross-sectional area divided into 15 grid blocks of 1 m thickness each.&#x20;

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption><p>Figure 10-4 Model system for examining migration of VOC from the vadose zone into an aquifer.</p></figcaption></figure>



The input file from TOUGH3/EOS7R can be directly used with minor modification by inserting a section with keyword "[MODDE](../../preparation-of-model-input/keywords-and-input-data/modde.md)".  This keyword provides basic model design parameters, including module to be run, type of initial condition input, thermophysical processes to be simulated and others.  In this simulation, the InitCType is given as "EOS7R", which tells the simulator to read the initial condition data  in the TOUGH3/EOS7R format and  the input file is originally provided for TOUGH3/EOS7R simulation. With such a input file, the gas and tracer definitions are not required. TOUGH4 will run the simulation with the same default gas and tracers,  one gas (AIR) and two tracers. The parameters for tracers are provided through "SELEC" keyword section as used in TOUGH3/EOS7R. &#x20;

Before the simulation of VOC migration, the initial condition of the flow system must be obtained by running a gravity-capillary equilibrium relative to the gas and capillary pressure conditions at water table. Details for system initialization simulation can be found in TOUGH3/EOS7R user manual.&#x20;

The simulation results are slightly different to the results from TOUGH3/EOS7R. This could be caused in the using of different gas solubility models.&#x20;

**Input Files:**    [input file](https://drive.google.com/file/d/1wZy5rKSxfW2EL9-0ZoAGk63ENoyfl6OL/view?usp=sharing)&#x20;

**Output Files:** [output files](https://drive.google.com/file/d/1Njug\_wT4PSuEIKweLbL9CYYtu8VtWWxm/view?usp=sharing)
