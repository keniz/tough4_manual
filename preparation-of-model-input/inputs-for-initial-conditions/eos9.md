# EOS9

Table 25. Primary Variables of EOS9

<table data-header-hidden><thead><tr><th></th><th width="70"></th><th width="77"></th><th width="82"></th><th></th></tr></thead><tbody><tr><td>Phase Conditions</td><td>PrV1</td><td>PrV2</td><td>PrV3</td><td>PrV4</td></tr><tr><td>Saturated Condition</td><td>Pw</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td></tr><tr><td>Unsaturated Condition</td><td>Sw</td><td>Xtr1</td><td>Xtr2</td><td>Xtr3</td></tr></tbody></table>

Table 25 shows the parameters of default initial conditions for EOS9. In the table, Xtrn is tracer _n_ mass fraction in the water.  Pw is the water pressure. Sw is water saturation. Xtr1-Xtr3 are optional. They are required only when the corresponding tracer component exists in the model. As a special case, the first primary variable may be initialized as PrV1 < 0, in which case it will be taken to denote capillary pressure, and will be converted internally to Swin the initialization phase.

&#x20;initCType =

&#x20;                   “EOS9”         reading the TOUGH3/EOS9 input files.
