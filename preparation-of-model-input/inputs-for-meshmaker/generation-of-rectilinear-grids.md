# Generation of rectilinear grids&#x20;

**XYZ**                invokes generation of a Cartesian (rectilinear) mesh.

Record **XYZ.l**           &#x20;

&#x20;                       Free format for 1 parameter or Format (E10.4)

&#x20;                       DEG

DEG                 angle (in degrees) between the Y-axis and the horizontal. If gravitational acceleration (parameter GF in record [PARAM](../keywords-and-input-data/param.md).2) is specified positive, -90° < DEG < 90° corresponds to grid layers going from top down. Grids can be specified from bottom layer up by setting GF or [BETAX](../keywords-and-input-data/conne.md) negative. Default (DEG = 0) corresponds to horizontal Y- and vertical Z-axis. X-axis is always horizontal.

Record **XYZ.2**          &#x20;

&#x20;                       Free format for 3 parameters or Format (A2, 3X, I5, E10.4)

&#x20;                       NTYPE, NO, DEL

NTYPE            set equal to NX, NY or NZ for specifying grid increments in X, Y, or Z direction.

NO                   number of grid increments desired.

DEL                 constant grid increment for NO grid blocks, if set to a non-zero value.

Record **XYZ.3**      (optional, DEL = 0. or blank only)

&#x20;                       Free format for as more as 20 parameters or Format (8E10.4)

&#x20;                       DEL(I), I = 1, NO

DEL(I)              a set of grid increments in the direction specified by NTYPE in record XYZ.2. Additional records with formats as XYZ.2 and XYZ.3 can be provided, with X, Y, and Z-data in arbitrary order.

Record **XYZ.4**    a blank record closes the XYZ data block.

Note that the end of block MESHMaker is also marked by a blank record. Thus, when MESHMaker/XYZ is used, there will be two blank records at the end of the corresponding input data block.
