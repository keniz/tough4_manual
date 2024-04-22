# CONNE

Keywork CONNE is used for define the connections of model mesh. It must be placed after the keyword ELEME.

**CONNE**            introduces information for the connections (interfaces) between elements.

Record **CONNE.1**

&#x20;                       Free format for 11 parameters

&#x20;                       ELNE1, ELNE2, NSEQ, NAD1, NAD2, ISOT, D1, D2, AREAX, BETAX, SIGX

&#x20;                       Or Format (A3, I2, A3, I2, 4I5, 5E10.4) (for 5 five-character element name only).

&#x20;                       EL1, NE1, EL2, NE2, NSEQ, NAD1, NAD2, ISOT, D1, D2, AREAX, BETAX, SIGX

_ELNE1_             first element name.

_ELNE2_            second element name.

_EL1_, _NE1_         code name of the first element (for formatted input only).

_EL2_, _NE2_        code name of the second element (for formatted input only).

_NSEQ_              number of additional connections in the sequence (used for formatted input only).

_NAD1_               increment of the code number of the first element between two successive connections sequence (used for formatted input only).

_NAD2_               increment of the code number of the second element between two successive connections (used for formatted input only).

_ISOT_               set equal to 1, 2, or 3; specifies absolute permeability to be _PER(ISOT)_ for the materials in elements (_ELNE1_) and (_ELNE2_), where _PER_ is read in block ROCKS. This allows assignment of different permeabilities, e.g., in the horizontal and vertical direction.

_D1_                   distance (m) from first element to interface.

_D2_                   distance (m) from second element to interface.

_AREAX_            interface area (m2).

_BETAX_            cosine of the angle between the gravitational acceleration vector and the line between the two elements. _GF_ × _BETAX_ > 0 (<0) corresponds to first element being above (below) the second element.

_SIGX_               “radiant emittance” factor for radiative heat transfer, which for a perfectly “black” body is equal to 1. The rate of radiative heat transfer between the two grid blocks is

&#x20;              $$G_{rad}=SIGX*\sigma_0*AREAX*(T_2^4-T_1^4)$$                                        (8-1)                                         &#x20;

where $$\sigma _0=5.6687e^{-8}J/m^2K^4s$$ is the Stefan-Boltzmann constant, and $$T_1$$and $$T_2$$ are the absolute temperatures of the two grid blocks. _SIGX_ may be entered as a negative number, in which case the absolute value will be used, and heat conduction at the connection will be suppressed. _SIGX_ = 0 will result in no radiative heat transfer.

Repeat record CONNE.1 for the number of connections desired.

Record **CONNE.2**        A blank record closes the CONNE data block. Alternatively, connection information may terminate on a record with ‘+++’ typed in the first three columns, followed by element cross-referencing information. This is the termination used when generating a MESH file with TOUGH4.

**Used in**: All EOS modules

**Example**:

_CONNE_                                                                // this is for input in the main input file

_A1001, A1002, 3\*0, 1, 0.150000E-05, 0.153200E+00, 0.188500E+03, 2\*0.0_

In the free format MESH file, TOUGH4 does not allow including NSEQ, NAD1, and NAD2 in input line:

_CONNE_                                                             &#x20;

_A1001, A1002, 1, 0.150000E-05, 0.153200E+00, 0.188500E+03, 2\*0.0_
