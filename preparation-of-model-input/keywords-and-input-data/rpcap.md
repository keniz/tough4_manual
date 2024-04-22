# RPCAP

**RPCAP**            introduces information on relative permeability and capillary pressure functions, which will be applied for all flow domains for which no data were specified in records ROCKS.1.2 and ROCKS.1.3. A catalog of relative permeability and capillary pressure functions is presented in [Appendix A](broken-reference) and [Appendix B](../../appendix/a-relative-permeability-functions/), respectively.

Record **RPCAP.1**

&#x20;                       Free format for 11 parameters, or Format (I5,5X,10E10.4)

&#x20;                       IRP, (RP(I), I = 1, 10)

_IRP_                   integer parameter to choose type of relative permeability function (see Appendix A).

_RP(I)_                I = 1, ..., 10 parameters for relative permeability function (Appendix A). I=8-10 are required only for IRP=12.

Record **RPCAP.2**

&#x20;                       Free format for 14 parameters, or Format (I5,5X,13E10.4)

&#x20;                       ICP, (CP(I), I = 1, 13)

_ICP_                 integer parameter to choose type of capillary pressure function (see Appendix B).

_CP(I)_            I = 1, ..., 13 parameters for capillary pressure function (Appendix B). I=8-13 are required only for ICP=12.

**Used in**: All EOS modules

**Example**:

_RPCAP_

_12, 0.917, 0.200, 0.200, 0.333, 1.000, 0.00, 0.97         // relative permeability_ [_function 12_](../../appendix/a-relative-permeability-functions/irp-12-regular-hysteresis.md)&#x20;

_12, 0.412, 0.030, 4.e3, 4.e5, 1.0, 0.412, 4.e3, 0.98, 0.0, 1.0e-06, 0.02, 0.0    // CAP_ [_function 12_](../../appendix/b-capillary-pressure-functions/icp-12-regular-hysteresis.md)

