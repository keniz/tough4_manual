# MODDE

**MODD**E         introduces model design parameters.

Record **MODDE.1**

&#x20;                       Free format for 3 parameters

&#x20;                       ModuleName, InitCType, EOSTypeS

_ModuleNam_   name of the EOS module will be run.

_InitCType_       the type of initial conditions. If not present, default type will be used. See Section "[Input for Initial Conduitions](../inputs-for-initial-conditions/)" for the initial condition type definition.

_EoSTypeS_      selection of the cubic EOS equation: PR, RK, or SRK, default is PR (for EOS7 and EWASG only).            &#x20;

Record **MODDE.2**

&#x20;                       Free format for 1 parameter

&#x20;                       ElemNameLength

&#x20;_ElemNameLength_    length of element name, can be 3-10, default length is 5 characters.

Record **MODDE.3**

&#x20;                       Free format for 5 bool type data

&#x20;                       n\_isoth, af\_diff, hBSW, hWBM, r2PH

_n\_isoth_            simulation in non-isothermal condition, TRUE or FALSE

_af\_diff_              accounting for diffusion in the simulation, TRUE or FALSE.

_hBSW_               Including brine (EOS7), salt (ECO2) or second water (EOS1) in the simulation, TRUE or FALSE (Default=TRUE).             &#x20;

_hWBM_              Including wellbore model in the simulation, TRUE or FALSE (Default=FALSE).             &#x20;

_r2PH_                Running ECO2 simulation in 2 phases (treat both gas and supercritical CO2 as “gas”, Default=3 phases).   TRUE or FALSE.             &#x20;

The keyword “MODDE” provides data block that reads the basic parameters for the model setup. If “MODDE” is present, it is suggested placing this keyword in front of most other keywords. If keyword “MULTI” is present, but no “MODDE”, the non\_isoth and af\_diff will be assigned based on inputs of “MULTI”. If keyword “MULTI” and “MODDE” both exist, please make sure they are consistent and place “MODDE” after “MULTI”. If MODDE" exists, "MULTI" is not required.&#x20;

**Used in**: All EOS modules

**Example**:

_MODDE_

_ECO2, ECO2M,              //  run ECO2 module, read ECO2M input file for initial condition_

_5                                       // length of gridblock name_&#x20;

_true; false; true; true; true       // use semicolon as separator is also allowed._                                 &#x20;

_// nonisothermal, no diffusion, including brine, wellbore simulation is on, in 2 phases_
