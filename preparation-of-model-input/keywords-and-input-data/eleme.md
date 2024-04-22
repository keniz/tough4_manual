# ELEME

**ELEME**            introduces element (grid block) information.

&#x20;Record **ELEME.1**

&#x20;                       Free format for 14 parameters.

&#x20;                       ELNE, NSEQ, NADD, MA12, VOLX, AHTX, PMX, X, Y, Z,

(USERX(I), I=1,3), Activity

Or Format (A3, I2, 2I5, A5, 9E10.4, A3) (for 5 five-character element name only)

&#x20;                       EL, NE, NSEQ, NADD, MA12, VOLX, AHTX, PMX, X, Y, Z,

(USERX(I), I=1,3), Activity

_ELNE_              element name, can be 3-10 characters.

_EL_, _NE_             five-character code name of an element. The first three characters are arbitrary, the last two characters must be numbers.

_NSEQ_              number of additional elements having the same volume and belonging to the same reservoir domain (used for formatted input only).

_NADD_               increment between the code numbers of two successive elements. (Note: the maximum permissible code number _NE_ + _NSEQ_ ×_NADD_ is ≤ 99. Used for formatted input only).

_MA12_              a five-character material identifier corresponding to one of the reservoir domains as specified in block ROCKS. If the first three characters are blanks and the last two characters are numbers then they indicate the sequence number of the domain as entered in ROCKS. If _MA12_ is left blank the element is by default assigned to the first domain in block ROCKS.

_VOLX_              element volume ( $$m^3$$).

_AHTX_               interface area ($$m^2$$) for linear heat exchange with semi-infinite confining beds. Internal MESH generation via MESHMaker will automatically assign _AHTX_.

_PMX_                 block-by-block permeability modification coefficient, $$\zeta _n$$ (optional). The _PMX_ may be used to specify spatially correlated heterogeneous fields. But users need to run their own geostatistical program to generate the fields they desire, and then use preprocessing programs to place the modification coefficients into the ELEME data block, as TOUGH4 provides no internal capabilities for generating such fields.

If a dummy domain ‘SEED’ is specified in data block ROCKS, it will be used as multiplicative factor for all the permeability parameters from block ROCKS (see Eq. 8-3), and strength of capillary pressure will be scaled according to Eq. 8-4. With a dummy domain ‘SEED’ in data block ROCKS, _PMX_ = 0 will result in an impermeable block.

In TOUGH4, _PMX_ can be active _without_ a dummy domain ‘SEED’ in the ROCKS block. If a dummy domain ‘SEED’ is not specified in data block ROCKS, it can be used to specify grid block permeabilities or permeability modifiers. If a positive value less than 1e-4 is given, it is interpreted as absolute permeability; if a negative value is provided, it is interpreted as a permeability modifier, i.e., a factor with which the absolute permeability specified in block ROCKS is multiplied. Alternatively, the same information can be provided through _USRX_ (columns 31–40) in block INCON.

If _PMX_ is blank for the first element, the element-by-element permeabilities are ignored. If a dummy domain ‘SEED’ is not specified in data block ROCKS, strength of capillary pressure will not be automatically scaled. Leverett scaling of capillary pressure can be applied with _MOP2(6)_ > 0 in data block MOMOP.

_X_, _Y_, _Z_             Cartesian coordinates of grid block centers. These may be included in the ELEME data to make subsequent plotting of results more convenient. Note that coordinates are used in TOUGH4 only in: optional initialization of a gravity-capillary equilibrium with EOS9 (see the addendum for EOS9), optional addition of potential energy to enthalpy with _MOP2(12)_ > 0 in data block MOMOP, and wellbore simulation.

_USERX(I)_     (optional) anisotropic permeability or permeability modifier of the X-, Y-, and Z-direction for I = 1, 2, and 3, respectively. Based on the values, TOUGH4 will internally determine whether it is permeability itself or permeability modifier. Alternatively, the same information can be provided through _USRX_ in block INCON. This input has become obsolete in TOUGH4, and it is retained for compatibility with TOUGH3. Users are encouraged to use the keyword SPAVA for input of the spatial variable parameters.&#x20;

_Activity_    (optional) element activity indicator. It can be “A”: active element, “I”: inactive element, “V”: time-dependent first-type boundary element, “T” constant temperature element. The default value is "A".&#x20;

Repeat record ELEME.1 for the number of elements desired.&#x20;

Record **ELEME.2**        A blank record closes the ELEME data block.

**Used in**: All EOS modules

**Example**:

_ELEME_                             // this is for input in the main input file

_A1435, 0\*2, 1, 0.619000E+12, 0.123800E+11, 0.0, 0.948000E+05, 0.0, -.500000E+02_

In the free format MESH file, TOUGH4 does not allow including NSEQ, NADD in input line:

_ELEME_

_A1435, 1, 0.619000E+12, 0.123800E+11, 0.0, 0.948000E+05, 0.0, -.500000E+02_
