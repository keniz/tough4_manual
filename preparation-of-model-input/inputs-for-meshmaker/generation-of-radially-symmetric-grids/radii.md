# RADII

**RADII**              is the first keyword following RZ2D/RZ2DL; it introduces data for defining a set of interfaces (grid block boundaries) in the radial direction.

Record **RADII.l**                   &#x20;

&#x20;                      Free format for 1 parameter or Format (I5)

&#x20;                      NRAD

NRAD             number of radius data that will be read. At least one radius must be provided, indicating the inner boundary of the mesh.

Record **RADII.2**, **RADII.3**, etc.

&#x20;                      Free format for as more as 20 parameters or Format (8E10.4)

&#x20;                      RC(I), I = 1, NRAD

RC(I)               a set of radii in ascending order.
