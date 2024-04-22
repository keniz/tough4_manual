# TIMES

**TIMES**            (optional) permits the user to obtain printout at specified times. This printout will occur in addition to printout specified in record PARAM.1.

&#x20;Record **TIMES.1**

&#x20;                       Free format for 4 parameters, or Format (2I5,2E10.4)

&#x20;                       ITI, ITE, DELAF, TINTER

_ITI_                   number of times provided on records TIMES.2, TIMES.3, etc.

_ITE_                  total number of times desired (_ITI_ ≤ _ITE_; default is _ITE_ = _ITI_).

_DELAF_            maximum time step size after any of the prescribed times have been reached (default is infinite).

_TINTER_           time increment for times with index _ITI_, _ITI_ +1, ..., _ITE_.

Record **TIMES.2**, **TIMES.3**, etc.

&#x20;                       Free format for as more as 20 parameters, or Format (20E10.4)

&#x20;                       (TIS(I), I = l, ITI)

_TIS(I)_       list of times (in ascending order) at which printout is desired.

_TIS (I)_ Input with multiple lines is allowed. The maximum number of input data for each line must be no more than 20. The maximum ITE is 100.&#x20;

**Used in**: All EOS modules

**Example**

_TIMES_

_3                                                                         // printout at 3 times_

_2.592e6, 31.5576e6, 63.1152e6                 // list of the 3 times_ at which printout is desired.
