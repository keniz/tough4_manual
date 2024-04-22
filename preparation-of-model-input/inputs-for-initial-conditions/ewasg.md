# EWASG

Table 27 Primary Variables of EWASG

<table data-header-hidden><thead><tr><th width="144"></th><th width="68"></th><th width="83"></th><th width="82"></th><th width="83"></th><th width="82"></th><th width="72"></th><th width="76"></th><th width="76"></th><th width="70"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td><td>PrV5</td><td>PrV6</td><td>PrV7</td><td>PrV8</td><td>PrV9</td><td>PrV10</td></tr><tr><td>Gas</td><td>Pg</td><td>Xg1</td><td>Xg2</td><td>Xg3</td><td>Xg4</td><td>Xs1</td><td>Xs2</td><td>Xs3</td><td>Xs4</td><td>T</td></tr><tr><td>Aqueous</td><td>Pa</td><td>Xg1</td><td>Xg2</td><td>Xg3</td><td>Xg4</td><td>Xs1</td><td>Xs2</td><td>Xs3</td><td>Xs4</td><td>T</td></tr><tr><td>Two-Phase</td><td>Pg</td><td>Sg+10</td><td>Xg2_G</td><td>Xg3_G</td><td>Xg4_G</td><td>Xs1</td><td>Xs2</td><td>Xs3</td><td>Xs4</td><td>T</td></tr></tbody></table>

Table 27 shows the parameters of default initial conditions for EWASG. In the table, Pg and Pa are pressure for gas and aqueous phase respectively. T is temperature. Xgn is the gas _n_ mass fraction in the existing phase.  Xgn\_G is the gas _n_ mass fraction in the gas phase excluding water vapor. Xsn is salt _n_ mass fraction in aqueous phase or in solid phase if no existence of aqueous phase. If Xs1>10.0, it will be the solid salt saturation plus 10.0.

&#x20;Xg2-Xg4, Xs2-Xs4 are optional. They are required only when the corresponding component exists in the model.

initCType =

&#x20;                   “EWASG”         reading the TOUGH3/EWASG input files.
