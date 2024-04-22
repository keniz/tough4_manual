# MINC processing for fractured media&#x20;

**MINC**              invokes postprocessing of a primary porous medium mesh from file MESH. The input formats in data block MINC are identical to those of the GMINC program (Pruess, 1983), with two enhancements: there is an additional facility for specifying global matrix-matrix connections (“dual permeability”); further, only active elements will be subjected to MINC-processing, the remainder of the MESH remaining unaltered as porous medium grid blocks.

**PART**             is the first keyword following MINC; it will be followed on the same line by parameters TYPE and DUAL with information on the nature of fracture distributions and matrix-matrix connections.

&#x20;                       Free format for 3 parameters or Format (2A5, 5X, A5)

&#x20;                       PART, TYPE, DUAL

PART              identifier of data block with partitioning parameters for secondary mesh.

TYPE              a five-character word for selecting one of the six different proximity functions provided in MINC (Pruess, 1983).

&#x20;             ONE-D:     a set of plane parallel infinite fractures with matrix block thickness between neighboring fractures equal to PAR(l).

&#x20;             TWO-D:    two sets of plane parallel infinite fractures, with arbitrary angle between them. Matrix block thickness is PAR(l) for the first set, and PAR(2) for the second set. If PAR(2) is not specified explicitly, it will be set equal to PAR(l).

&#x20;             THRED:     three sets of plane parallel infinite fractures at right angles, with matrix block dimensions of PAR(l), PAR(2), and PAR(3), respectively. If PAR(2) and/or PAR(3) are not explicitly specified, they will be set equal to PAR(l) and/or PAR(2), respectively.

&#x20;             STANA:     average proximity function for rock loading of Stanford large reservoir model (Lam et al._,_ 1988).

&#x20;             STANB:     proximity function for the five bottom layers of Stanford large reservoir model.

&#x20;             STANT:      proximity function for top layer of Stanford large reservoir model.

Note: a user wishing to employ a different proximity function than provided in MINC needs to replace the function subprogram PROX(x) in file Mesh\_Maker.f90 with a routine of the form:

&#x20;                  _FUNCTION PROX(x)_

&#x20;                        _PROX = (arithmetic expression in x)_

&#x20;                  _RETURN_

&#x20;                  _END_

It is necessary that PROX(x) is defined even when _x_ exceeds the maximum possible distance from the fractures, and that PROX = 1 in this case. Also, when the user supplies his/her own proximity function subprogram, the parameter TYPE has to be chosen equal to ONE-D, TWO-D, or THRED, depending on the dimensionality of the proximity function. This will assure proper definition of innermost nodal distance (Pruess, 1983).

DUAL               is a five-character word for selecting the treatment of global matrix matrix flow.

&#x20;                        blank:      (default) global flow occurs only through the fracture continuum, while rock matrix and fractures interact locally by means of interporosity flow (“double-porosity” model).

&#x20;                        MMVER:    global matrix-matrix flow is permitted only in the vertical; otherwise like the double-porosity model; for internal consistency this choice should only be made for flow systems with one or two predominantly vertical fracture sets.

&#x20;                         MMALL:    global matrix-matrix flow in all directions; for internal consistency only two continua, representing matrix and fractures, should be specified (“dual-permeability”).

Record **PART.l**                    &#x20;

&#x20;                        Free format for 10 parameters or Format (2I3, A4, 7E10.4)

&#x20;                       J, NVOL, WHERE, (PAR(I), I = 1, 7)

J                       total number of multiple interacting continua.

NVOL               total number of explicitly provided volume fractions (NVOL < J). If NVOL < J, the volume fractions with indices NVOL+l, ..., J will be internally generated; all being equal and chosen such as to yield proper normalization to 1.

WHERE            specifies whether the sequentially specified volume fractions begin with the fractures (WHERE = ‘OUT ‘) or in the interior of the matrix blocks (WHERE = 'IN  ').

PAR(I)               I = 1, 7 holds parameters for fracture spacing (see above).

Record **PART.2.1**, **2.2**, etc.   &#x20;

&#x20;                       Free format for as more as 20 parameters or Format (8E10.4)

&#x20;                       (VOL(I), I = 1, NVOL)

VOL(I)             volume fraction (between 0 and 1) of continuum with index I (for WHERE = ‘OUT ‘) or index J + l – I (for WHERE = ‘IN  ‘). NVOL volume fractions will be read. For WHERE = ‘OUT ‘, I = 1 is the fracture continuum, I = 2 is the matrix continuum closest to the fractures, I = 3 is the matrix continuum adjacent to I = 2, etc. The sum of all volume fractions must not exceed 1.
