# ECO2

Table 26. Primary Variables of ECO2

<table data-header-hidden><thead><tr><th width="177"></th><th width="71"></th><th width="76"></th><th width="75"></th><th width="76"></th><th width="80"></th><th width="73"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td><td>PrV7</td></tr><tr><td>Gas</td><td>Pg</td><td>Xco2</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Xco2</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Liquid</td><td>Pl</td><td>Xco2</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Aqueous-Gas</td><td>Pg</td><td>Sg</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Liquid-Gas</td><td>Pg</td><td>Sg</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>Ytot</td></tr><tr><td>Aqueous-Liquid</td><td>Pl</td><td>Sl</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>T</td></tr><tr><td>Three Phases</td><td>Pg</td><td>Sg</td><td>Xnacl</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td><td>Sa</td></tr></tbody></table>

Table 26 shows the parameters of default initial conditions for ECO2. In the table, Pg, Pa and pl are pressure for gas, aqueous liquid phase respectively. Xtrn is the tracer _n_ mass fraction in the user specified phase.  Xnacl is salt mass fraction in aqueous phase or solid saturation Ss+10. Sa, Sg, and Sl are saturation of aqueous, gas and liquid phase, respectively. Ytot is total water mass fraction in both liquid and gas CO2 phase.  T is temperature. Xnacl and Xtr1-Xtr3 are optional. They are required only when the corresponding component exists in the model.

User can use other set parameters as the initial conditions through initCType in input data record MODDE.1 or command line –i \<parameter>

&#x20;initCType =

&#x20;                   “ECO2N”         reading the TOUGH3/ECO2N input files.

&#x20;                   “ECO2M”        reading the TOUGH3/ECO2M input files.

&#x20;                   “ECO2NV2”    reading the TOUGH3/ECO2N V2 input files.

&#x20;                   “ECO2NTR”    reading the TOUGHREACT/ECO2N INCON files.
