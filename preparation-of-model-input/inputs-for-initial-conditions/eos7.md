# EOS7

Table 24 Primary Variables of EOS7

<table data-header-hidden><thead><tr><th width="144"></th><th width="78"></th><th width="84"></th><th width="89"></th><th width="87"></th><th width="89"></th><th width="71"></th><th width="82"></th><th width="87"></th><th width="89"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td><td>PrV7</td><td>PrV8</td><td>PrV9</td><td>PrV10</td></tr><tr><td>Gas</td><td>Pg</td><td>Xg1</td><td>Xg2</td><td>Xg3</td><td>Xg4</td><td>Xbr</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Xg1</td><td>Xg2</td><td>Xg3</td><td>Xg4</td><td>Xbr</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Two-Phase</td><td>Pg</td><td>Sg+10</td><td>Xg2_G</td><td>Xg3_G</td><td>Xg4_G</td><td>Xbr</td><td>Xtr1_G</td><td>Xtr2_G</td><td>Xtr3_G</td><td>T</td></tr><tr><td><p>Two-phase</p><p>(Alternative)</p></td><td>Pg</td><td>Sg+10</td><td>Xg2_A</td><td>Xg3_A</td><td>Xg4_A</td><td>Xbr</td><td>Xtr1_A</td><td>Xtr2_A</td><td>Xtr3_A</td><td>T</td></tr></tbody></table>

Table 24 shows the parameters of default and alternative initial conditions for EOS7. In the table, Pg and Pa are pressure for gas and aqueous phase respectively. Xgn and Xtrn are the gas _n_ and tracer _n_ mass fractions in the existing phase, respectively. T is temperature. Xbr is brine mass fraction in aqueous phase. Xgn\_G and Xtrn\_G are the gas _n_ and tracer _n_ mass fractions in the gas phase excluding water vapor, respectively. Xgn\_A and Xtrn\_A are the gas _n_ and tracer _n_ mass fractions in the aqueous phase, respectively. Xbr, Xg2-Xg4, Xtr1-Xtr3 are optional. They are required only when the corresponding component exists in the model.

User can use other set parameters as the initial conditions through defining initCType in input data record MODDE.1 or command line _–i \<parameter>_

&#x20;initCType =

&#x20;                   “EOS7”         reading the TOUGH3/EOS7 input files.

&#x20;                   “EOS7R”       reading the TOUGH3/EOS7R input files.

&#x20;                   “EOS7C”      reading the TOUGH3/EOS7C input files.

&#x20;                  “EOS7CA”     reading the TOUGH3/EOS7CA input files.

&#x20;                   “EOS7MG”   reading the TOUGH3/EOS7MG INCON files.

&#x20;                  "SPEOS7”     using alternative parameters for two-phase condition (Table 24, last row).
