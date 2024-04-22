# FOFT

**FOFT**               (optional) introduces a list of elements (grid blocks) for which time-dependent data are to be written out for plotting during the simulation. A separate file is generated for each element in CSV format. The name of each file starts with FOFT, and includes the element name. If regular or simple hysteresis is invoked via _IRP_ = _ICP_ = 12 or _IRP_ = _ICP_ = 13, then relevant hysteresis parameters are also written to FOFT.

&#x20;Record **FOFT.1**

Free format for 2 parameters, or Format (A5,5X,I5)

&#x20;                       EFOFT, IFOFTF

&#x20;_EFOFT_            element name.

_IFOFTF_          a flag to control the amount of printout.

&#x20;       0:         default printout of pressure, temperature, and saturation of flowing phases.

&#x20;       \>0:       phase number, print out mass fraction of each component in the specified phase in addition to the default printout.

<0:       print out mass fraction of each component in each of all the flowing phases in addition to the default printout.

Record **FOFT.2**

A blank record closes the FOFT data block. Repeat records FOFT.l for as many elements as desired.

If the input keyword is in lower case “foft” or “foft\_”, an alternative input for this record is provided. A list of as many as 20 element names in each line in free format will be read, and IFOFTF is set to 0. Multiple lines are allowed.

**Used in**: All EOS modules

**Example**:

_FOFT_

_AAAA1, 1_

_AAAA2, -1_

or:

_foft\__

_AAAA1, AAAA2, AAAA3_
