# Problem 2 - Heat Sweep in a Vertical Fracture (rvf)

The present problem is designed to study thermal interference along preferential flow paths (fractures), by modeling nonisothermal injection into and production from a single vertical fracture, as illustrated in Figure 10-1 (from Pruess and Bodvarsson, 1984). The fracture is bounded by semi-infinite half-spaces of impermeable rock, which provide a conductive heat supply. Initial temperature is 300 ˚C throughout. Water at 100 ˚C temperature is injected at one side of the fracture at a constant rate of 4 kg/s, while production occurs at the other side against a specified wellbore pressure.&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Figure 10-1 Schematic diagram of injection-production system in vertical fracture. Injection occurs at I, production at P.</p></figcaption></figure>

Details of this example can be found in [EOS1 manual](https://drive.google.com/file/d/19jQ5UnMi8XPlm6PZp59NQr2p6D8Y55DZ/view?usp=drive\_link), sample 2 (rvf).

A special feature of the problem is that the [semi-analytical method](../../governing-equations/semi-analytical-conductive-heat-exchange.md) is used to describe heat conduction in the confining layers, reducing the dimensionality of the problem from 3-D to 2-D. This feature is invoked by setting MOP(15) = 1. Water remains in single-phase liquid conditions throughout, so that no data block RPCAP for relative permeabilities and capillary pressures is needed.&#x20;

The problem is run in three separate segments.&#x20;

(1) A first run performs mesh generation only, using the MESHMaker/XYZ module. For this run, the data records from MESHM through ENDFI in the input file are inserted right behind the first record with the problem title. The mesh consists of 12 horizontal by 10 vertical blocks of 20 m x 20 m. Ordinarily, we would specify NX = 12 and NZ = 10 to make such a mesh; however, special considerations arise here because we desire appropriate surface areas for heat conduction to be placed in the MESH file. By default, in the MESHMaker/XYZ module the interface areas with impermeable confining beds are always taken to be in the X-Y plane, so that in a mesh with vertical Z-axis the interface areas for conductive heat transfer would be assigned to the top and bottom boundaries. To properly assign the desired lateral heat transfer areas, the mesh is generated as an X-Y mesh (NX = 12, NY = 10, NZ = 1), and the Y-axis is specified to make an angle of 90˚ with the horizontal, i.e., to point in the vertical direction. The MESHMAKER input terminates on ENDFI, to bypass the flow simulation and to limit processing to mesh generation only.

(2) The second processing step calculates a hydrostatic pressure equilibrium in the fracture under isothermal conditions.

The generated MESH file in first run needs to be edited, and a dummy element of large volume is appended at the end of the ELEME block, to provide the thermal data for the conductive boundaries. This element belongs to domain CONBD with appropriate rock density, thermal conductivity, and specific heat, and it will be initialized with the default conditions of 300 ˚C temperature. The final SAVE file generation from this run will be used as the initial condition for the next run.

(3)  The subsequent production/injection run uses the SAVE file produced by the gravity equilibration run which is renamed to INCON and used for initialization. The specified maximum time of $$1.57788 \times 10^{8}$$seconds (5 years) is reached after 15-time steps. The simulation results are presented in the output files.

**Input file for run segment 1**: [INFILE](https://drive.google.com/file/d/1AVgqlQuGmiuajSbCt9e0ZeFTj2BaJ5gq/view?usp=sharing)

**Input files for run segment 2**: [Input\_files\_hydrostatic.zip](https://drive.google.com/file/d/1alAoVppNo8zNCcjmxUTYJyJD0Sn0S\_y9/view?usp=sharing)

**Input files for run segment 3**: [input\_files.zip](https://drive.google.com/file/d/1cKZpz6hp15\_JfI1jPr32c5LqrMbJZqQC/view?usp=sharing)         **output files**: [output\_fles.zip](https://drive.google.com/file/d/1yMdRnsadXsMLtb8OKQtAb9hJbVIyQ59j/view?usp=sharing)
