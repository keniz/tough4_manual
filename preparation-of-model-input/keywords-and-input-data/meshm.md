# MESHM

**MESHM**            introduces parameters for internal mesh generation and processing with MESHMaker.

The MESHMaker input has a modular structure which is organized by keywords. Detailed instructions for preparing MESHMaker input are given in the section "Inputs for MESHMAKER".

Record **MESHM.1**

&#x20;                       Free Format or Format (A5)

&#x20;                       WORD

_WORD_                          enter one of several keywords, such as RZ2D, RZ2DL, XYZ, MINC, to generate different kinds of computational meshes. For details of mesh generation inputs, users may refer to the Sections "[Geometry Data](../geometry-data/)" and "[Inputs for MESHMAKER](../inputs-for-meshmaker/)"&#x20;

Record **MESHM.2**       A blank record closes the MESHM data block.

**Used in**: All EOS modules
