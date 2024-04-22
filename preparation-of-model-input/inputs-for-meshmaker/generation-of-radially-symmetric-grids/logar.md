# LOGAR

**LOGAR**ithmic   introduces data on radial increments that increase from one to the next by the same factor ($$\Delta R_{n+1}=f\cdot\Delta R_n$$).

Record **LOGAR.1**                 &#x20;

&#x20;                       free format for 3 parameters or Format (I5, 5X, 2E10.4)

&#x20;                       NLOG, RLOG, DR

NLOG              number of additional interface radii desired.

RLOG              desired radius of the last (largest) of these radii.

DR                   reference radial increment: the first DR generated will be equal to f • DR, with f internally determined such that the last increment will bring total radius to RLOG.      f < 1 for decreasing radial increments is permissible. If DR is set equal to zero, or left blank, the last increment DR generated before keyword LOGAR will be used as default.

Additional blocks RADII, EQUID, and LOGAR can be specified in arbitrary order.

Note: At least one radius must have been defined before LOGAR can be invoked. If DR = 0, at least two radii must have been defined.
