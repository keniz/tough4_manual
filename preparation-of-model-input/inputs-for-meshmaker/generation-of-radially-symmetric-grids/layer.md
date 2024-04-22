# LAYER

**LAYER**            introduces information on horizontal layers, and signals closure of RZ2D input data.

Record **LAYER. l**    &#x20;

&#x20;                       Free format for 1 parameter or Format (I5)

&#x20;                       NLAY

NLAY              number of horizontal grid layers.

Record **LAYER.2**                 &#x20;

&#x20;                       Free format for as more as 20 parameters or Format (8E10.4)

&#x20;                       H(I), I = 1, NLAY

H(I)                   a set of layer thicknesses, from top layer downward. By default, zero or blank entries for layer thickness will result in assignment of the last preceding non-zero entry. Assignment of a zero layer thickness, as needed for inactive layers, can be accomplished by specifying a negative value.

The LAYER data close the RZ2D data block. Note that one blank record must follow to indicate termination of the MESHM data block. Alternatively, keyword MINC can appear to invoke MINC-processing for fractured media (see [below](https://app.gitbook.com/o/q9ZXQz7vu1Vs1ySDfJ5L/s/s4vEX2gTEyZWPZd8id3C/\~/changes/61/preparation-of-model-input/inputs-for-meshmaker/minc-processing-for-fractured-media)).
