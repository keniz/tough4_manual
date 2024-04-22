# EOS1

Table 19 Primary Variables of EOS1

<table data-header-hidden><thead><tr><th width="148"></th><th width="68"></th><th width="83"></th><th width="75"></th><th width="75"></th><th width="71"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td></tr><tr><td>Gas</td><td>Pg</td><td>Xw2</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Xw2</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Two-Phase</td><td>Pg</td><td>Sg+10</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>Xw2</td></tr><tr><td>Supercritical</td><td>dw</td><td>Xw2</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr></tbody></table>

The parameters used as default initial conditions are the identical set of parameters of primary variables.   Table 19 shows the parameters of default initial conditions/primary variables for EOS1 with three tracers. In the table, Pg and Pa are pressure for gas and aqueous phase respectively. T is temperature. Xtrn is tracer _n_ mass fraction in the user specified phase (see[ ](../keywords-and-input-data/tracr.md)_TracerInPhase_  in [tracer definition](../keywords-and-input-data/tracr.md)).  Xw2 is water2 mass fraction in existing phase. For two phase flow, the water2 mass fraction is assumed to be the same in both phases. Sg is gas saturation. dw is the water density in supercritical condition. Xw2 and Xtr1-Xtr3 are optional. They are required only when the corresponding mass component exists in the model.

User can use alternative set parameters as the initial conditions through defining initCType in input data record MODDE.1 or command line _–i \<parameter>_

&#x20;initCType =

&#x20;                   “EOS1”          reading the TOUGH3/EOS1 input files.

The TOUGH3/EOS1 initial conditions provided in the input file will be transformed internally into TOUGH4/EOS1 initial conditions.
