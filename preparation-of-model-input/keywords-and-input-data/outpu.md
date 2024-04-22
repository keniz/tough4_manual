# OUTPU

**OUTPU**            permits the users to obtain printout of specified variables (optional). OUTPU specifications will supersede the default condition specified in _KDATA_ in data block PARAM.&#x20;

&#x20;Record **OUTPU.0**        (optional)

&#x20;                       Free format for 1 string parameter, or Format(A20)

&#x20;                       COUTFM

_**COUTFM**_          a keyword indicating the desired output format, currently either CSV, TECPLOT, or PETRASIM

Record **OUTPU.1**

&#x20;                       Free format for 1 parameter, or Format(I5)

&#x20;                       MAXOUTVAR

_**MOUTVAR**_       number of variables to be printed out.

Record **OUTPU.2**, **OUTPU.3**, …, **OUTPU.(1+**_**MOUTVAR**_**)**

&#x20;                       Free format for 3 parameters, or Format(A20,2I5)

&#x20;                       COUTLN, ID1, ID2

_COUTLN_          name of variable, to be chosen among the available options. They include primary variables, secondary parameters, flow terms, and more. The name of variables is all capital letters and should be typed in the input file as shown in Table 18.

_ID1_                 first option for the corresponding keyword in _COUTLN_, as shown in Table 18.

_ID2_                 second option for the corresponding keyword in _COUTLN_, as shown in Table 18.

&#x20;

Table 18. Keywords of block OUTPU and related output variables

<table data-header-hidden><thead><tr><th width="184"></th><th width="96"></th><th width="69"></th><th width="333"></th></tr></thead><tbody><tr><td>Keyword</td><td>ID1</td><td>ID2</td><td>Output Variable</td></tr><tr><td>SET</td><td>ISET</td><td>-</td><td><p>Prints predefined sets of output variables.</p><p>ISET = 1:   Set of main element-related output variables</p><p>ISET = 2:   Set of main connection-related output variables</p><p>ISET = 3:   Set of main generation-related output variables</p></td></tr><tr><td>NO COMMA</td><td>-</td><td>-</td><td>Omit commas between values</td></tr><tr><td>NO QUOTES</td><td>-</td><td>-</td><td>Omit quotes around values</td></tr><tr><td>NO NAME</td><td>-</td><td>-</td><td>Omit element names</td></tr><tr><td><p>COORDINATE</p><p>COORD</p></td><td>NXYZ</td><td>-</td><td><p>Grid-block or connection coordinates;</p><p>mesh dimension and orientation are automatically determined, or can be specified through variable NXYZ:</p><p>NXYZ = 1   : Mesh is 1D  “X  ”</p><p>NXYZ = 2   : Mesh is 1D  “ Y ”</p><p>NXYZ = 3   : Mesh is 1D  “  Z”</p><p>NXYZ = 4   : Mesh is 2D  “XY ”</p><p>NXYZ = 5   : Mesh is 2D  “X Z”</p><p>NXYZ = 6   : Mesh is 2D  “ YZ”</p><p>NXYZ = 7   : Mesh is 3D  “XYZ”</p></td></tr><tr><td>INDEX</td><td>-</td><td>-</td><td>Index (running number) of elements, connections, or sinks/sources</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td><p>MATERIAL</p><p>ROCK</p><p>ROCK TYPE</p></td><td>-</td><td>-</td><td>Material number</td></tr><tr><td><p>MATERIAL NAME</p><p>ROCK NAME</p><p>ROCK TYPE NAME</p></td><td>-</td><td></td><td>Material name</td></tr><tr><td><p>ABSOLUTE</p><p> </p></td><td>ISOT</td><td>-</td><td>Absolute permeability in direction ISOT; if ISOT = 0, permeabilities related to all three directions are printed</td></tr><tr><td>POROSITY</td><td>-</td><td>-</td><td>Porosity</td></tr><tr><td>TEMPERATURE</td><td>-</td><td>-</td><td>Temperature</td></tr><tr><td>PRESSURE</td><td>IPH#</td><td>-</td><td>Pressure of phase IPH</td></tr><tr><td>SATURATION</td><td>IPH#</td><td>-</td><td>Saturation of phase IPH</td></tr><tr><td>RELATIVE</td><td>IPH#</td><td>-</td><td>Relative permeability of phase IPH</td></tr><tr><td>VISCOSITY</td><td>IPH#</td><td>-</td><td>Viscosity of phase IPH</td></tr><tr><td>DENSITY</td><td>IPH#</td><td>-</td><td>Density of phase IPH</td></tr><tr><td>ENTHALPY</td><td>IPH#</td><td>-</td><td>Enthalpy of phase IPH</td></tr><tr><td>CAPILLARY</td><td>IPH#</td><td>-</td><td><p>Capillary pressure;</p><p>if IPH = 1, difference between gas and aqueous phase pressures (for ECO2, difference between gaseous CO2 and aqueous phase pressures);</p><p>if IPH=2, difference between gas-NAPL phase pressures for TMVOC, and difference between gaseous and liquid CO2 phase pressures for ECO2</p></td></tr><tr><td>MASS FRACTION</td><td>IPH</td><td>IC</td><td>Mass fraction of component IC in phase IPH</td></tr><tr><td>DIFFUSION1</td><td>IPH#</td><td>-</td><td>Diffusion parameter group 1 ( ) of phase b = IPH</td></tr><tr><td>DIFFUSION2</td><td>IPH#</td><td>-</td><td>Diffusion parameter group 2 ( ) of phase b = IPH</td></tr><tr><td>PSAT</td><td>-</td><td>-</td><td>Saturated vapor pressure</td></tr><tr><td>BIOMASS</td><td>-</td><td>-</td><td>Biomass concentration</td></tr><tr><td>PRIMARY</td><td>IPV</td><td>-</td><td>Primary variable No. IPV; if IPV = 0, all NK+1 primary variables are printed</td></tr><tr><td>SECONDARY</td><td>IPH#</td><td>ISP</td><td><p>Secondary parameter No. ISP related to phase IPH, where</p><p>ISP = 0 : All secondary parameters</p><p>ISP = 1  : Phase saturation</p><p>ISP = 2  : Relative permeability</p><p>ISP = 3  : Viscosity</p><p>ISP = 4  : Density</p><p>ISP = 5  : Enthalpy</p><p>ISP = 6  : Capillary pressure</p><p>ISP = 7  : Diffusion parameter group 1</p><p>ISP = 8  : Diffusion parameter group 2</p></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td><p>TOTAL FLOW</p><p>TOTAL FLOW RATE</p></td><td>-</td><td>-</td><td>Total flow rate</td></tr><tr><td><p>FLOW</p><p>RATE</p><p>FLOW RATE</p></td><td>IPH</td><td>IC</td><td><p>Advective flow rate.</p><p>IPH=0;      IC=0:     Total flow</p><p>IPH>0;      IC=0:     Flow of phase IPH</p><p>IPH&#x3C;0;      IC=0:     Flow of each phase</p><p>IPH>0;      IC>0:     Flow of component IC in phase IPV</p><p>IPH>0;      IC&#x3C;0:     The flow of each component in phase IPH</p></td></tr><tr><td>DIFFUSIVE FLOW</td><td>IPH</td><td>IC</td><td><p>Diffusive flow rate.</p><p>IPH=0;      IC=0:     Total flow</p><p>IPH>0;      IC=0:     Flow of phase IPH</p><p>IPH&#x3C;0;      IC=0:     Flow of each phase</p><p>IPH>0;      IC>0:     Flow of component IC in phase IPH</p><p>IPH>0;      IC&#x3C;0:     The flow of each component in phase IPH</p></td></tr><tr><td>HEAT FLOW</td><td>-</td><td>-</td><td>Heat flow rate</td></tr><tr><td>VELOCITY</td><td>IPH#</td><td>-</td><td>Flow velocity of phase IPH</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td><p>GENERATION</p><p>GENEARTION RATE</p></td><td>-</td><td>-</td><td>Production or injection rate</td></tr><tr><td>FLOWING ENTHALPY</td><td>-</td><td>-</td><td>Flowing enthalpy</td></tr><tr><td>FRACTIONAL FLOW</td><td>IPH#</td><td>-</td><td>Fractional flow of phase IPH (production only)</td></tr><tr><td>WELLBORE RESSURE</td><td>-</td><td>-</td><td>Wellbore pressure (wells on deliverability only)</td></tr></tbody></table>

&#x20;_# If IPH = 0, the output variables of all phases are printed._

**Used in**: All EOS modules

**Example**:

_OUTPU_

_4_&#x20;

_PRESSURE_

_TEMPERATURE_&#x20;

_SATURATION, 2_&#x20;

_MASS FRACTION,  1,  2_
