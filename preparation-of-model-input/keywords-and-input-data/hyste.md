# HYSTE

**HYSTE**            (optional) provides numerical controls on the hysteretic characteristic curves. It is not needed if the default values of all its parameters are to be used.

Record **HYSTE.1**

&#x20;                   Free format for 3 parameters, or Format(3I5).

&#x20;                   IEHYS(I), I=1,3

_IEHYS(1)_     flag to print information about hysteretic characteristic curves.

&#x20;                   \=0         no additional print out.

&#x20;                   ≥1          print a one-line message to the output file every time a capillary-pressure branch switch occurs (recommended).&#x20;

_IEHYS(2)_     flag indicating when to apply capillary-pressure branch switching.

&#x20;                   \=0        after convergence of time step (recommended).

&#x20;                   \>0        after each Newton-Raphson iteration.

_IEHYS(3)_     run parameter for sub-threshold saturation change.

&#x20;                   \=0        no branch switch unless |_∆S_| > _CP(10)._

&#x20;                   \>0        allow branch switch after run of _IEHYS(3)_ consecutive time steps for which all |_∆S_| < _CP(10)_ and all _∆S_ are the same sign. Recommended value 5-10. This option may be useful if the time step is cut to a small value due to convergence problems, making saturation changes very small.

The IEHYS(1)-IEHYS(3) can also be inputted through IE(5), IE(6) and IE(7), if the hysteresis function is on.

**Used in**: All EOS modules

**Example**:

_HYSTE_

_0, 1, 0_
