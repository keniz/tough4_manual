# GOFT

**GOFT**               (optional) introduces a list of sinks/sources for which time-dependent data are to be written out for plotting during the simulation. A separate file is generated for each sink/source in CSV format. The name of each file starts with GOFT, and includes the sink/source name.

Record **GOFT.1**

&#x20;                       Free format for 2 parameters, or Format (A5,5X,5X,I5)

&#x20;                       EGOFT, IGOFTF                  &#x20;

_ECOFT_            the name of an element in which a sink/source is defined.

_IGOFTF_           a flag to control the amount of printout.

&#x20;                       0:         default printout of mass flow rate and flowing enthalpy.     &#x20;

&#x20;                       \>0:       print out fractional mass flow rate of the specified phase in addition to the default. printout.

&#x20;                       <0:       print out fractional mass flow rate of each of all the flowing phases in addition to the default printout.

Record **GOFT.2**

A blank record closes the GOFT data block. Repeat records GOFT.l for as many sinks/sources as desired.

If the input keyword is in lower case “goft” or “goft\_”, an alternative input for this record is provided. A list of as many as 20 ECOFT in each line in free format will be read, and IGOFTF is set to 0. Multiple lines are allowed.

**Used in**: All EOS modules

**Example**:

_GOFT_

_AAA01, 1                               //write out time series of gas rate for the well at "AAA01"._ &#x20;
