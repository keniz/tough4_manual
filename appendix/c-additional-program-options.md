# ☑️ C: ADDITIONAL PROGRAM OPTIONS

TOUGH4 provides more additional options through arrays IE and FE. The flexible input for IE and FE makes the use of these options very easy. Their inputs are through keywork [SELEC](../preparation-of-model-input/keywords-and-input-data/selec.md).  Some IE and FE elements with lower subscripts have been used for module specific inputs, which may have different purposes for different EOS modules. For details, users may refer to the specific input requirements for each EOS module in the "[Process Modeling](../process-modeling/)" section. The default values for both IE and FE are 0. Followings are the list of additional options:

**IE(17)**               allows choice of different mass balance output&#x20;

0:                      Output mass balance for the whole system only.

\-1:                     Output mass balance for all rocks and the whole system.

n (n>0):           Output mass balance for rock _n_ and the whole system.

**IE(18)**               controls the impact of solid on permeability (effect for ECO2 and EWASG only).

0:                      no impact.

1:                       the impact is on, see [EWASG process modeling](../process-modeling/ewasg.md) for details.

**IE(19)**               Accounts water vapor for real gas property (effect for EOS7 and EWASG only).

0:                      True.

1:                       False.

**IE(20)**             allows choice of different random number generator

0:                      use FORTRAN pseudorandom number RANDOM\_NUMBER.

1:                       use TOUGH2 internal random number generator.

**IE(21)**             Multiplies the linear equation of each element by inverse of its diagonal matrix (the diagonal term will be all 1.0 after multiplication) . This may avoid error in solving linear equations.&#x20;

0:                     True.  &#x20;

1:                       False.

**IE(22)**              Selects ECO2 simulation phase conditions (equivalent to the input of [MODDE 3.4](../preparation-of-model-input/keywords-and-input-data/modde.md)) .

0:                      in 3 phases&#x20;

1:                       in 2 phases (treat both gas and supercritical CO2 as “gas”).  &#x20;

**IE(23)**              &#x20;

**IE(24)**             allows to turn vapor pressure lowering on/off. It can be overridden by specific inputs of EOS4 and EWASG module for VPL on/off option.&#x20;

0: VPL is off.&#x20;

1: VPL is on.

**IE(25)**             The input for tracer distribution coefficient (_XKD1)_ and fraction of organic carbon (_FOCM_) through [_ROCKS.1.1_](../preparation-of-model-input/keywords-and-input-data/rocks.md) is conflict for TMVOC. For maintaining the compatibility of input file from TOUGH3/TMVOC and other TOUGH4 modules, IE(25) is used to coordinate the inputs. The input is through lot 6-10 of ROCKS.1.1. (for TMVOC only)

0:                    lot 6 is for FOCM input, lot7-lot10 for XKD1-XKD4 input.

1:                     lot 6-10 is for XKD1-XKD5 input, no FOCM input.&#x20;

**IE(26)**             Checks whether wellbore flow turns direction (wellbore simulation only).&#x20;

0: off.&#x20;

1: on.

**IE(27)**             Selects calculation method for thermal conductance along wellbore (for wellbore simulation only)&#x20;

0: no special treatment, in the same way as in porous media.

1: ignore the conductive heat flow.

2: consider conduction in well wall only.

3: Fully consider conduction in fluids and well wall.&#x20;

**IE(28)**             Accounts for mist flow (wellbore simulation only).&#x20;

0: on.&#x20;

1: off.

**IE(29)**             Applies calculated geothermal gradient to (wellbore simulation only):&#x20;

0: wellbore grid elements only.&#x20;

1: all model grid elements.

**IE(30)**             Inputs the frequency for scanning the file "[Update\_Simulation\_Parameters](../preparation-of-model-input/adjustment-of-computing-parameters-at-run-time.md)" to see if this file has been updated during run time. The default frequency is 1000, which means the code will check the file every 1000 time steps.

**IE(31)**             Selects the effects of water on the thermophysical properties of the CO2-rich phase (for ECO2 only).&#x20;

0: ignore the impact of water on the density and viscosity of the CO2-rich phase.&#x20;

1: fully consider impact of water on the CO2-rich phase thermophysical properties.

\-1: ignore the impact of water on density, viscosity and enthalpy of CO2-rich phase (IE(31)=-1 is compatible with ECO2N v1.0).&#x20;

**IE(32)**             Selects decay mass for mass balance calculation.&#x20;

0: decay mass calculated from current time step parameters.

1:  use average of decay mass calculated from previous and current time steps.&#x20;

**IE(33)**             Performs supercritical water simulation

0: on.&#x20;

1: off, supercritical water is neglected and treated as high temperature vapor.

**IE(34)**             Adjusts calculated CO2 enthalpy using the analytical solution by Altunin et al. (1975) to match the value from NIST Chemistry Web Book

0: no adjustment (compatible with ECO2N V1.0).&#x20;

1: do the adjustment to match NIST reference state (If you use enthalpy data from NIST Chemistry Web Book as input for source/sinks, IE(34) must be 1.

**IE(50)**              Number of the pressure points (allow 50-1000) in the table of CO2 thermophysical properties. (See [ECO2 process modeling](../process-modeling/eco2.md) for details)

**IE(51)**               number of the temperature points (allow 50-1000) in the table of CO2 thermophysical properties.

**IE(111)**            Selects thermodynamic formulation.

0:                     IFC-67; for subcritical conditions only&#x20;

1:                      IAPWS-IF97&#x20;

2:                     IAPWS-IF97 for T<800°C, IAPWS-95 for T≥800°C





