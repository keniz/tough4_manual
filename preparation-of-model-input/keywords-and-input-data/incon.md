# INCON

**INCON**            introduces element-specific initial conditions.

&#x20;Record **INCON.1**

&#x20;                      Free format for 8 parameters

&#x20;                      ELNE, NSEQ, NADD, PORX, stateName, (perm(I), I=1,3)

&#x20;                      Or Format (A3, I2, 2I5, E15.9, A3, 3E10.4) (for mesh with 5-character gird name only)

&#x20;                      EL, NE, NSEQ, NADD, PORX, stateName, (perm(I), I=1,3)

_ELNE_             the element name (for free format)

_EL_, _NE_           code name of element (for formatted input)

_NSEQ_            number of additional elements with the same initial conditions. (Not used in free format input)

_NADD_            increment between the code numbers of two successive elements with identical initial conditions. . (Not used in free format input)

_PORX_            porosity; if zero or blank, porosity will be taken as specified in block ROCKS if option START is used.

_stateName_    phase state name. It is important only when the program cannot figure out its phase state through the primary variables.

_perm(i)_   grid block permeability, i=1,2 and 3 for x, y, z direction, respectively (optional).

Record **INCON.2**        specifies primary variables.

&#x20;                      Free format for as more as 12 parameters， or Format (4E20.14)

&#x20;                      Xl, X2, X3, ...

A set of primary variables for the element specified in record INCON.l. INCON specifications will supersede default conditions specified in PARAM.5, and domain-specific conditions that may have been specified in data block INDOM. Different sets of primary variables are used for different EOS modules; see the description of EOS modules in their corresponding sections. For formatted input, when more than four primary variables are used, input with multiple lines (records) are required.

&#x20;Record **INCON.3**

A blank record closes the INCON data block. Alternatively, initial condition information may terminate on a record with ‘+++’ typed in the first three columns, followed by time stepping information. This feature is used for a continuation run from a previous TOUGH3 simulation.

**Used in**: All EOS modules

**Example**:

_// an initial condition for EOS7 with 2 gases and brine, in two-phase condition (AQG)_

_INCON_

_A11 1, , , 3.50009259E-01, AQG_                                    &#x20;

_0.4201733403239E+07, 0.8115861911613E-01, 0.3072090574758E-05, 0.0\*2, 65_&#x20;

_// the variables are: pressure, gas saturation, gas1 mass fraction in gas phase, gas 2 mass fraction in_&#x20;

_// gas phase, brine mass fraction and temperature._

In main input FILE, additional two lots after element name for NSEQ, NADD are required for compatible with TOUGH3 input.  In INCON file, NSEQ and NADD are not required:

_A11 1, 3.50009259E-01, AQG_&#x20;
