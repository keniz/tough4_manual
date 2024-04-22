# Active Fracture Modle

### 1. Active Fracture Concept

There is evidence that only a portion of the connected fracture network conducts water under unsaturated conditions. The fractures contributing to liquid flow are referred to as “active fractures”. The Active Fracture Concept (AFC) was developed by Liu et al. (1998) to describe gravity-dominated, non-equilibrium, preferential liquid flow in fractures, which is expected to be similar to fingering in unsaturated porous media. AFC is based on the hypothesis that (1) the number of active fractures is small compared with the total number of connected fractures, (2) the number of active fractures within a grid block is large so that the continuum approach is valid, and (3) the fraction of active fractures, , is related to water flux and equals one for a fully saturated system, and zero if the system is at residual saturation. The following power function of effective liquid saturation, , fulfills these conditions:

&#x20;

&#x20;

Here,  is a positive constant depending on properties of the fracture network, and  is the effective liquid saturation given by

&#x20;

&#x20;

Capillary pressure and relative permeability functions are modified to account for the fact that the effective saturation in the active fractures, , is larger than the effective saturation of the total fracture continuum:

&#x20;

&#x20;

Using the van Genuchten model, capillary pressure and liquid relative permeability are given, respectively, by

&#x20;

&#x20;

and

&#x20;

&#x20;

The fracture-matrix interface area reduction factor is given by

&#x20;

&#x20;

The AFC is invoked by selecting , which is provided as an additional parameter of the standard van Genuchten model (ICP=7) through variable _CP_(6,_NMAT_). Fracture-matrix interface area reduction is invoked by selecting ISOT between -10 and -12 (see Table 10).

&#x20;

&#x20;

\


&#x20;

### C.2. Reduction of Fracture-Matrix Interface Area

There is evidence that fracture-matrix interaction in the unsaturated zone is reduced as a result of fracture coatings as well as preferential flow in the fractures as invoked by flow instabilities (fingering) and small-scale heterogeneities. A number of options for reducing fracture-matrix interface area have been implemented for use in a dual-permeability flow simulation. Interface area reduction is applied to connections with a negative value for variable _ISOT_, which is provided in the CONNE block. Different modifiers are used depending on the value of _ISOT_ and _MOP_(8) as summarized in Table 10.

&#x20;

Table 10. Option for Reducing Fracture-Matrix Interface Area

<table data-header-hidden><thead><tr><th width="456.3333333333333"></th><th width="93"></th><th></th></tr></thead><tbody><tr><td><em>ISOT</em></td><td><em>MOP</em>(8)</td><td>Interface area reduction factor</td></tr><tr><td>positive</td><td>any</td><td>No interface area reduction, i.e.,</td></tr><tr><td>negative</td><td>1</td><td></td></tr><tr><td>-1, -2, -3</td><td><p>0</p><p>2</p></td><td></td></tr><tr><td>-4, -5, -6</td><td><p>0</p><p>2</p></td><td></td></tr><tr><td>-7, -8, -9</td><td>0</td><td></td></tr><tr><td>-10, -11, -12</td><td>0</td><td> (see Appendix C.1)</td></tr><tr><td><p>                      :       Fracture-matrix interface area reduction factor.</p><p>                       :       For flow of phase b, upstream saturation of phase b.</p><p>                       :       For flow of phase b, upstream relative permeability of phase b.</p><p>    :       6th parameter of rel. perm. function of upstream element;</p><p>                                    if zero (i.e., not specified), reset to one.</p></td><td></td><td></td></tr></tbody></table>

&#x20;

&#x20;
