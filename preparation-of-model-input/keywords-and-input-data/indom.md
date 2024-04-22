# INDOM

**INDOM**            introduces domain-specific initial conditions. These will supersede default initial conditions specified in PARAM.4, and can be overwritten by element-specific initial conditions in data block INCON.&#x20;

&#x20;Record **INDOM. l**

&#x20;                      Free format for 2 parameters, or Format (A5, 2X, A3)

&#x20;                       MAT, StateName

&#x20;

_MAT_                 name of a reservoir domain, as specified in data block ROCKS.

_StateName_      (optional) phase state name with 3 characters. It is needed only when the system cannot figure out its phase state through the primary variables.

&#x20;Record **INDOM.2**

&#x20;                       Free format for as more as 12 parameters, Format (4E20.13)

&#x20;                       Xl, X2, X3, ...

A set of primary variables assigned to all grid blocks in the domain specified in record INDOM.l. Different sets of primary variables are used for different EOS modules; see the description of EOS modules. For formatted input, when more than four primary variables are used, more than one line (record) must be provided.

Record **INDOM.3**

A blank record closes the INDOM data block. Repeat records INDOM.l and INDOM.2 for as many domains as desired. The ordering is arbitrary and need not be the same as in block ROCKS.

**Used in**: All EOS modules

**Example**:

_INDOM                                 // an example for ECO2, no brine, with 2 tracers, in aqueous condition_

_ROCK1_

_0.4E+07, 0.0\*3, 85.0     // pressure, mass fraction for CO2, tracer1, and tracer2, and temperature_
