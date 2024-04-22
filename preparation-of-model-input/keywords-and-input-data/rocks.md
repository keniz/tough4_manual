# ROCKS

**ROCKS**            introduces material parameters for different reservoir domains.

&#x20;Record **ROCKS.1**

&#x20;                       Free Format for 9 parameters, or Format (A5, I5, 7E10.4)

&#x20;                       MAT, NAD, DROK, POR, (PER (I), I = 1,3), CWET, SPHT

_MAT_               material name (rock type). In wellbore simulation, the rock name for the wellbore cell must start with the letter “w” or “x”, where “w” indicates normal (open) wellbore cell whereas “x” indicates the wellbore cells filled with porous medium;

_NAD_                 if zero or negative, defaults will take effect for a number of parameters (see below);

&#x20;                       ≥1: will read another data record to override defaults.

&#x20;                       ≥2: will read two more records with domain-specific parameters for relative permeability and capillary pressure functions.

_DROK_               rock grain density (kg/m3). If _DROK_ is set to a very large value (typically 1.0E50), a constant _temperature_ boundary condition can be specified (but variable pressure/saturation). &#x20;

_POR_                 default porosity (void fraction) for all elements belonging to domain “_MAT_" for which no other porosity has been specified in block INCON.&#x20;

_PER(I)_              I = 1,3 absolute permeabilities along the three principal axes, as specified by _ISOT_ in block CONNE.

_CWET_              formation heat conductivity under fully liquid-saturated conditions (W/m ˚C).

_SPHT_               rock grain specific heat (J/kg ˚C). Domains with _SPHT_ > $$10^4$$J/kg ˚C will not be included in global material balances. This provision is useful for boundary nodes, which are given very large volumes so that their thermo-dynamic state remains constant. Because of the large volume, inclusion of such nodes in global material balances would make the balances useless.

Some specific rock names may have special meanings. When a (dummy) domain named “SEED” is specified, the absolute permeabilities specified in _PER(I)_ are modified by the block-by-block permeability modifiers (PM) according to

$$k_n\rarr k_n'=k_n*\zeta_n$$                                                                                      (8-5)

&#x20;                                                                                                                                                                                               Here, $$\kappa_n$$ is the absolute (“reference”) permeability of grid block _n_, as specified in data block ROCKS for the domain to which that grid block belongs, is the modified permeability, and $$\zeta_n$$ is the PM coefficient. When PM is in effect, the strength of capillary pressure will be automatically scaled according to (Leverett, 1941)

$$P_{cap,n}\rarr P_{cap,n}'=P_{cap,n}/\sqrt{\zeta_n}$$                                                                   (8-6)                                                                                                            &#x20;

No grid blocks should be assigned to this domain; the presence of domain ‘SEED’ simply serves as a flag to put permeability modification into effect. Random (spatially uncorrelated) PM data can be internally generated in TOUGH4. Alternatively, externally defined permeability modifiers may be provided as part of the geometry data (_PMX_) in block ELEME. Available PM options are:

(1)   externally supplied           :  $$\zeta_n=PMX-PER(2)$$

(2)   “linear”                              :   $$\zeta_n=PER(1)\times s-PER(2)$$

(3)   “logarithmic”                    :    $$\zeta_n=e^{-PER(1)\times s}-PER(2)$$     &#x20;

where _s_ is a random number between 0 and 1

Data provided in domain ‘SEED’ are used to select the following options.

_DROK_              random number seed for internal generation of "linear" permeability modifiers.

&#x20;                       \= 0: (default) no internal generation of "linear" permeability modifiers.

&#x20;                       \> 0: perform "linear" permeability modification; random modifiers are generated internally with _DROK_ as seed.

_POR_                 random number seed for internal generation of "logarithmic" permeability modifiers

&#x20;                       \= 0: (default) no internal generation of "logarithmic" permeability modifiers.

&#x20;                       \> 0: perform "logarithmic" permeability modification; random modifiers are generated internally with _POR_ as seed.

Note if both _DROK_ and _POR_ are specified as non-zero, _DROK_ takes precedence. And if both _DROK_ and _POR_ are zero, permeability modifiers as supplied through ELEME data will be used.

_PER(1)_             scale factor (optional) for internally generated permeability modifiers.

&#x20;                       \= 0: (defaults to _PER(1)_ = 1): permeability modifiers are generated as random numbers in the interval (0, 1).

&#x20;                       \> 0: permeability modifiers are generated as random numbers in the interval (0, _PER(1)_).

_PER(2)_             shift (optional) for internal or external permeability modifiers.

&#x20;                       \= 0: (default) no shift is applied to permeability modifiers.

&#x20;                       \> 0: permeability modifiers are shifted according to  =  – _PER(2)_. All  < 0 are set equal to zero.

Note that the domain ‘SEED’ is not required in TOUGH4 if externally defined permeability modifiers in block ELEME are used without any shift.

Other specific rock names:

(1)   “REFCO”, input density, viscosity and compressibility at the reference pressure, temperature at data lot 5, 6, 7, 3, and 4, respectively. This is used by EOS9 only.

(2)   “GEOTH”, input reference elevation, temperature, and geothermal gradient at data lot 5, 6, and 7. This is used for wellbore simulation only.

(3)   “QLOSS”, input parameters for analytical solution of radial heat exchange between fluids in a wellbore and the surrounding formation for option MOP(15)=5. Details of the parameters for input can be found at the discussion for [MOP(15)](param.md) input.&#x20;

Record **ROCKS.1.1**     (optional, NAD ≥ 1 only)

&#x20;                       Free format for 10 parameters, or Format (10E10.4)

&#x20;                       COM, EXPAN, CDRY, TORTX, GK, XKD1-XKD5 (FOCM)

&#x20;_COM_               pore compressibility (Pa-1),     $$(1/\phi)(\partial \phi/\partial P)_T$$            (default is 0).

_EXPAN_             pore expansivity (1/ ˚C),           $$(1/\phi)(\partial \phi/\partial P)_P$$            (default is 0).

_CDRY_               formation heat conductivity under desaturated conditions (W/m ˚C), (default is _CWET_).

_TORTX_            tortuosity factor for binary diffusion. If _TORTX_ = 0, a porosity and saturation-dependent tortuosity will be calculated internally from the Millington and Quirk (1961) model, Eq. (4-11). When diffusivities, _FDDIAG_ in data block DIFFU, are specified as negative numbers, $$\tau_0\tau_\beta=S_\beta$$will be used.

_GK_                   Klinkenberg parameter b ( $$Pa^{-1}$$) for enhancing gas phase permeability                                 according to the relationship _kgas_ = _k_ \* (1 + _b_/_P_).

_XKD1-5_           Distribution coefficients for as more as 5 tracers in current rock, in the aqueous phase, $$m^3kg^{-1}$$. Distribution coefficients can also be inputted through key word “TRACR” for specific tracer.

_FOCM_             fraction of organic carbon present in domain; used for calculating amount of VOC adsorbed. _FOCM_ is used only in TMVOC. _FOCM_ shares the same input data lot with _XKD1_. This conflict may be avoided through IE(25), see [Appendix C](../../appendix/c-additional-program-options.md). The purpose of remaining this option is to maintain the compatibility of input file for TMVOC and other modules from TOUGH3.

Record **ROCKS.1.2**     (optional, NAD ≥ 2 only)

&#x20;                       Free format for 11 parameters, or Format (I5, 5X,7E10.4)

&#x20;                       IRP, (RP(I), I= 1,10)

&#x20;_IRP_                 integer parameter to choose type of relative permeability function (see Appendix A).

_RP(I)_               I = 1, ..., 10 (use free format)  or 7 (use formatted input) parameters for relative permeability function ([Appendix A)](broken-reference).&#x20;

Record **ROCKS.1.2.1**  (optional, IRP = 12, and use the formatted input only)

&#x20;                       Format (3E10.4)

&#x20;                       RP(I), I= 8,10

_RP(I)_                I = 8, ..., 10 parameters for relative permeability function ([Appendix A](broken-reference)).      &#x20;

Record **ROCKS.1.3**     (optional, NAD ≥ 2 only)

&#x20;                       Free format for 14 parameters, or Format (I5, 5X,7E10.4)

&#x20;                       ICP, (CP(I), I = 1,13)

_ICP_                  integer parameter to choose type of capillary pressure function (see [Appendix B](../../appendix/a-relative-permeability-functions/)).

_CP(I)_               I = 1, ..., 13 (for free format) or 7 (for formatted input) parameters for capillary pressure function ([Appendix B](../../appendix/a-relative-permeability-functions/)).

&#x20;Record ROCKS.1.3.1  (optional, ICP = 12, formatted input only)

&#x20;                       Format (6E10.4)

&#x20;                       CP(I), I = 8,13

_CP(I)_               I = 8, ..., 13 parameters for capillary pressure function (Appendix B).

Record **ROCKS.1.4**    (optional, IRP=40 and ICP=40 only)

&#x20;                      Free format for 1 parameter

&#x20;                      Num\_Sg

_Num\_Sg_         The total number of gas saturations (rows) for the input table of relative permeability and capillary pressure.

Record **ROCKS.1.4.1**  (optional, Num\_Sg>0 only)

&#x20;                      Free format for 4 parameters, or Format (4E10.4)

&#x20;                      Sg, kg, kw, pc

_sg_                   gas saturation.

_kg_                   relative permeability in gas phases corresponding to gas saturation sg.

_kw_                  relative permeability in aqueous phases corresponding to gas saturation sg.

_pc_                   capillary pressure corresponding to gas saturation sg.

Repeat record 1.4.1 for Num\_Sg times.

Repeat records 1, 1.1, 1.2, 1.2.1., 1.3, 1.3.1, 1.4, and 1.4.1 for different reservoir domains.

Record **ROCKS.2**        A blank record closes the ROCKS data block.

**Used in**: All EOS modules

**Example**:

_ROCKS_

_SANDY, 2, 2500., 1.e-4, 1.e-12\*3, 2.5 ,1000.             //ROCKS.1_

_1.e-8, , , 0.25                                                                    //ROCKS.1.1_&#x20;

_1,  0.,  0.,  1.,  1.,                                                               //ROCKS.1.2_

_8                                                                                        //ROCKS.1.3_
