# EOS2

Table 20. Primary Variables and alternative initial conditions for EOS2

<table data-header-hidden><thead><tr><th width="154"></th><th width="81"></th><th width="84"></th><th width="86"></th><th width="94"></th><th width="87"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td></tr><tr><td>Gas</td><td>Pg</td><td>Pco2</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Pco2</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Two-Phase</td><td>Pg</td><td>Sg+10</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>Pco2</td></tr><tr><td><p><em>Gas</em></p><p><em>(Alternative)</em></p></td><td><em>Pg</em></td><td><em>Xco2</em></td><td><em>Xtr1</em></td><td><em>Xtr2</em></td><td><em>Xtr3</em></td><td><em>T</em></td></tr><tr><td><p><em>Aqueous</em></p><p><em>(Alternative</em></p></td><td><em>Pa</em></td><td><em>Xco2</em></td><td><em>Xtr1</em></td><td><em>Xtr2</em></td><td><em>Xtr3</em></td><td><em>T</em></td></tr><tr><td><p><em>Two-phase</em></p><p><em>(Alternative)</em></p></td><td><em>Pg</em></td><td><em>Sg+10</em></td><td><em>Xtr1</em></td><td><em>Xtr2</em></td><td><em>Xtr3</em></td><td><em>T</em></td></tr></tbody></table>

Table 20 shows the parameters of default or alternative initial conditions for EOS2. In the table, Xtrn is tracer _n_ mass fraction in the user specified phase.  Xco2 is CO2 mass fraction in existing phase. Pg and Pa are pressure for gas and aqueous phase respectively. T is temperature. Pco2 is CO2 partial pressure. Xtr1-Xtr3 are optional. They are required only when the corresponding tracer component exists in the model.

User can use alternative set parameters as the initial conditions through defining initCType in input data record MODDE.1 or command line _–i \<parameter>_

&#x20;initCType =

&#x20;                   “EOS2”              reading the TOUGH3/EOS2 input files.

&#x20;                   “SPEOS2”          using an alternative set parameter as initial conditions (the last 3 lines, Table 20).
