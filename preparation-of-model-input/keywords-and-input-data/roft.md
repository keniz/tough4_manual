# ROFT

**ROFT**             (optional) introduces a list of pairs of rocks for which time-dependent data for them are to be written out for plotting during the simulation. A separate file is generated for each pair of rocks in CSV format. The name of each file starts with ROFT and includes the pair of two rock names.

Record **ROFT.1**

&#x20;                       Free format for 2 parameters, or Format (A10,10X,I5)

&#x20;                       EROFT, IROFTF                            &#x20;

_**EROFT**_            a pair of rock names, i.e., an ordered pair of two rock names (no blank between elements).

_**IROFTF**_           a flag to control the amount of printout.

&#x20;                       0:         default printout of heat flux and flow rate of each flowing phase.

&#x20;                      \>0:       print out fractional mass flow of each component in the specified phase in addition to the default printout.

&#x20;                      <0:       print out fractional mass flow of each component in each of all the flowing phases in addition to the default printout.

Record **ROFT.2**

A blank record closes the ROFT data block. Repeat records ROFT.l for as many connections as desired.

**Used in**: All EOS modules

**Example**:

_ROFT_

_ROCK1ROCK2, 1_

_SAND1SOIL2, -1_
