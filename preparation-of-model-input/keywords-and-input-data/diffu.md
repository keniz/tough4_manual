# DIFFU

**DIFFUSION** (optional; needed only when _accounting\_for\_diffusion_ is true) introduces diffusion coefficients.

&#x20;Record **DIFFU.1**

&#x20;                       Free format for 4 or less parameters, Format (4E10.4)

&#x20;                       FDDIAG(I,1), I=1,NPH

&#x20;                       diffusion coefficients for mass component # 1 in all phases (I=1: gas; I=2: aqueous; etc.)

Record **DIFFU.2**

&#x20;                       Free format for 4 or less parameters, Format (4E10.4)

&#x20;                       FDDIAG(I,2), I=1,NPH

&#x20;                       diffusion coefficients for mass component # 2 in all phases (I=1: gas; I=2: aqueous; etc.)

Provide a total of _NumCom_ records with diffusion coefficients for all _NumCom_ mass components.

**Used in**: All EOS modules, except EOS9

**Example**: (gas, liq.)

_DIFFU_                    //diffusivity data for two phases, five mass components

&#x20;_1.e-6; 1.e-10          // use semicolon as separator is also allowed._        &#x20;

&#x20;_0.e-6, 0.e-6_

&#x20;_1.e-6, 1.e-10_

&#x20;_1.e-6, 1.e-10_

&#x20;_1.e-6, 1.e-10_
