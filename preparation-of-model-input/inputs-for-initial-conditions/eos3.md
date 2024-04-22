# EOS3

Table 21. Primary Variables of EOS3

<table data-header-hidden><thead><tr><th width="145"></th><th width="77"></th><th width="83"></th><th width="71"></th><th width="74"></th><th width="71"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td></tr><tr><td>Gas</td><td>Pg</td><td>Xair</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Xair</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Two-Phase</td><td>Pg</td><td>Sg+10</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr></tbody></table>

Table 21 shows the parameters of default initial conditions for EOS3. In the table, Xtrn is tracer _n_ mass fraction in the user specified phase. Pg and Pa are pressure for gas and aqueous phase respectively. T is temperature. Xair is air mass fraction in existing phase.  Xtr1-Xtr3 are optional. They are required only when the corresponding tracer component exists in the model.

User can use alternative set parameters as the initial conditions through defining initCType in input data record MODDE.1 or command line _–i \<parameter>_

&#x20;initCType =

&#x20;                   “EOS3”          reading the TOUGH3/EOS3 input files.

&#x20;                   “EOS4”          reading the TOUGH3/EOS4 input files.

&#x20;                    “EOS7"         reading the TOUGH3/EOS7 input files, neglect the brine.
