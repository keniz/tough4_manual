# PARAM

**PARAM**            introduces computation parameters, time stepping information, and default initial conditions.

&#x20;Record **PARAM.1**

&#x20;                       Free format for 33 parameters, or Format (2I2, 3I4, 24I1, 10X, 2E10.4, 2I5).

&#x20;                       NOITE, KDATA, MCYC, MSEC, MCYPR, (MOP(I), I = 1, 24), TEXP, BE, SAVE\_Fq,          &#x20;

&#x20;                       TimeS\_Fq

_NOITE_            specifies the maximum number of Newtonian iterations per time step (default is 8)

_KDATA_            specifies amount of printout (default is 1).

&#x20;                       0 or 1: print a selection of element variables.

&#x20;                       2: in addition, print a selection of connection variables.

&#x20;                       3: in addition, print a selection of generation variables.

If the above values for _KDATA_ are increased by 10, printout will occur after each Newton-Raphson iteration (not just after convergence). If negative values are used, printout for the selection of variables will be generated in the file format of TECPLOT. The amount of printout is given by the absolute value of _KDATA_.

_MCYC_              maximum number of time steps to be calculated.&#x20;

_MSEC_              maximum duration, in CPU seconds, of the simulation (default is infinite).

_MCYPR_            printout will occur for every multiple of _MCYPR_ steps (default is 10000).

_MOP(I)_             I = 1,24 allows choice of various options, which are also documented in printed output from a TOUGH4 run.

_MOP(1)_           if unequal 0, a short printout for non-convergent iterations will be generated.

_MOP(2)_ through _MOP(6)_    generate additional printout in various sub-routines, if set unequal 0. This feature should not be needed in normal applications, but it will be convenient when a user suspects a bug and wishes to examine the inner workings of the code. The amount of printout increases with _MOP(I)_ (consult source code listings for details).

_MOP(2)_          TimeStepping (main subroutine).

_MOP(3)_          In subroutines for mass accumulation and flux calculations.

_MOP(4)_          No longer used in TOUGH4.

_MOP(5)_          Subroutines for equation of state calculations.

_MOP(6)_          No longer used.

_MOP(7)_          if unequal 0, a printout of input data will be provided.

_MOP(8)_          if _ISOT_ < 0, chooses the option for reducing fracture-matrix interface area (See Appendix D).

_MOP(9)_         determines the composition of produced fluid with the MASS option (see GENER, below). The relative amounts of phases are determined as follows:

&#x20;                       0:         according to relative mobilities in the source element.

&#x20;                       1:         produced source fluid has the same phase composition as the producing element.

_MOP(10)_       chooses the interpolation formula for heat conductivity as a function of liquid saturation (Sl)

&#x20;                       0:         C(Sl) = CDRY + SQRT(Sl)\* \[CWET - CDRY]

&#x20;                       1:         C(Sl) = CDRY + Sl \* (CWET - CDRY)

_MOP(11)_       determines evaluation of mobility and permeability at interfaces.

&#x20;                      0:         mobilities are upstream weighted with WUP (see PARAM.3),                       permeability is upstream weighted.

&#x20;                       1:         mobilities are averaged between adjacent elements, permeability is             upstream weighted.

&#x20;                       2:         mobilities are upstream weighted, permeability is harmonic weighted.

&#x20;                       3:         mobilities are averaged between adjacent elements, permeability is            harmonic weighted.

&#x20;                       4:         mobility and permeability are both harmonic weighted.

_MOP(12)_       determines interpolation procedure for time dependent sink/source data (flow rates and enthalpies).

&#x20;                       0:         triple linear interpolation; tabular data are used to obtain interpolated rates and enthalpies for the beginning and end of the time step; the average of these values is then used.

&#x20;                       1:          step function option; rates and enthalpies are taken as averages of the table values corresponding to the beginning and end of the time step.

&#x20;                       2:         rigorous step rate capability for time dependent generation data.

A set of times $$t_i$$ and generation rates $$q_i$$ provided in data block GENER is interpreted to mean that sink/source rates are piecewise constant and change in discontinuous fashion at table points. Specifically, generation is assumed to occur at constant rate  $$q_i$$during the time interval \[ $$t_i$$ ,  $$t_{i+1}$$ ], and changes to  $$q_{i+1}$$ at $$t_{i+1}$$. Actual rate used during a time step that ends at time _t_, with  $$t_i$$_≤ t_ ≤  $$t_{i+1}$$, is automatically adjusted in such a way that total cumulative exchanged mass at time _t is_

&#x20;      $$Q(t) = \int _0^tqdt'=\sum_{j=1}^{i-1}q_j(t_{j+1}-t_j)+q_i(t-t_i)$$                                   (8-4)&#x20;

is rigorously conserved. If also tabular data for enthalpies are given, an analogous adjustment is made for fluid enthalpy, to preserve $$\int qhdt$$.

_MOP(13)_       determines content of INCON and SAVE files.

&#x20;                       0:         standard content.

&#x20;                       1:         writes user-specified initial conditions to file SAVE, including permeabilities.&#x20;

&#x20;                       2:         reads parameters of hysteresis model from file INCON.

_MOP(14)_       (void)

_MOP(15)_       determines conductive heat exchange with impermeable geologic formations using semi-analytical methods (see Section "[Semi-Analytical Conductive Heat Exchange](../../governing-equations/semi-analytical-conductive-heat-exchange.md)").

&#x20;                       0:         heat exchange is off.

&#x20;                       1:         linear heat exchange between a reservoir and confining beds is on (for grid blocks that have a non-zero heat transfer area; see data block [ELEME](eleme.md)). Initial temperature in cap- or base-rock is assumed uniform and taken as the temperature with which the last element in data block ELEME is initialized.

&#x20;                       2:        linear heat exchange _between a reservoir and confining beds_ is on. Initial temperature for the confining bed adjacent to an element that has a non-zero heat transfer area is taken as the temperature of that element in data block INCON.

Heat capacity and conductivity of the confining beds are specified in block ROCKS for the particular domain to which the very last volume element in data block ELEME belongs. Thus, if a semi-analytical heat exchange calculation is desired, the user would append an additional dummy element of a very large volume at the end of the ELEME block, and provide the desired parameters as initial conditions and domain data, respectively, for this element. It is necessary to specify which elements have an interface area with the confining beds, and to give the magnitude of this interface area. This information is input as parameter _AHTX_ of volume element data in block ELEME (data lot 11). Volume elements for which a zero-interface area is specified will not be subject to heat exchange.

&#x20;                      5:         radial heat exchange between fluids in a wellbore and the surrounding formation is on. Constant well and formation properties are given in a material named QLOSS with the following parameters:

&#x20;             _DROK_: Rock grain density \[kg/m3] of formation near well

&#x20;             _POR_: Well radius \[m]

&#x20;            _PER(1)_: Reference elevation \[m]; specify Z coordinate in block ELEME, Columns 71–80

&#x20;             _PER(2)_: Reference temperature \[°C]

&#x20;             _PER(3)_: Geothermal gradient \[°C/m]

&#x20;             _CWET_: Heat conductivity \[W/kg °C] of formation near well

&#x20;             _SPHT_: Rock grain specific heat \[J/kg °C] of formation near well

&#x20;                      6:         radial heat exchange _between fluids in a wellbore and the surrounding formation_ is on. Depth-dependent well and formation properties (depth, radius, temperature, conductivity, density, capacity) are provided on an external file named _radqloss.dat_ with the information in the following format:

On the first line, _NMATQLOSS_ is the number of elevations with geometric and thermal data, and _NMATQLOSS_ lines are provided with the following data in free format: elevation \[m], well radius \[m], initial temperature \[°C], _CWET_, _DROK_, _SPHT_. Between elevations, properties are calculated using linear interpolation.

RESTART is possible for linear heat exchange between a reservoir and confining beds (_MOP(15)_= 1 or 2), but not for radial heat exchange (_MOP(15)_= 5 or 6).  The data necessary for continuing the linear heat exchange calculation in a TOUGH4 continuation run are written onto a text file named TABLE. When restarting a simulation run, this file has to be present in the working folder. If file TABLE is absent, TOUGH4 assumes that no prior heat exchange with confining beds has taken place.

_MOP(16)_       provides automatic time step control.

&#x20;                    0:         automatic time stepping based on maximum change in saturation.

&#x20;                    1:         automatic time stepping based on number of iterations needed for convergence.

&#x20;                    \>1:       time step size will be doubled if convergence occurs within _ITER_ ≤ _MOP(16)_ Newton-Raphson iterations. It is recommended to set _MOP(16)_ in the range of 2 - 4.

_MOP(17)_       handles time stepping after linear equation solver failure.

&#x20;                    0:         reduce time step after linear equation solver failure.

&#x20;                    \>0:         no time step reduction despite linear equation solver failure.

_MOP(18)_       selects handling of interface density.

&#x20;                     0:         perform upstream weighting for interface density.

&#x20;                     \>0:       average interface density between the two grid blocks. However, when one of the two phase saturations is zero, upstream weighting will be performed.

_MOP(19)_       switch used by different EOS modules for conversion of primary variables. It is effect only for EOS3, EOS4, and EOS6. See Section "[Inputs for Initial Conditions](../inputs-for-initial-conditions/)" for details.

_MOP(20)_       switch for vapor pressure lowering in EOS4; _MOP(20)_=1 optionally suppresses vapor pressure lowering effects. Users may use IE(24) to turn on the vapor pressure lowering for other EOS modules.&#x20;

_MOP(21)_       (void)&#x20;

_MOP(22)_       (void)

_MOP(23)_       (void)

_MOP(24)_       determines handling of multiphase diffusive fluxes at interfaces.

&#x20;                       0:         harmonic weighting of fully coupled effective multiphase                            diffusivity.

&#x20;                       1:         separate harmonic weighting of gas and liquid phase diffusivities.

_TEXP_               parameter for temperature dependence of gas phase diffusion coefficient.

_BE_                   (optional) parameter for effective strength of enhanced vapor diffusion; if set to a non-zero value, will replace the parameter group for vapor diffusion (see Eq. (4-9).

SAVE\_Fq       The frequency for writing out SAVE file. SAVE file will be written every SAVE\_Fq time step.

TimeS\_Fq      The frequency for writing time series output. Time series output file will be written every TimeS\_Fq time step, Default is 1.

Record **PARAM.2**

Free format for 8 parameters, Format (4E10.4, A5, 5X, 3E10.4)

TSTART, TIMAX, DELTEN, DELTMX, ELST, GF, REDLT, SCALE

_TSTART_          starting time of simulation in seconds (default is 0).

_TIMAX_            time in seconds at which simulation should stop (default is infinite).

_DELTEN_          length of time steps in seconds. If _DELTEN_ is a negative integer, _DELTEN_ = -_NDLT_, the program will proceed to read _NDLT_ records with time step information. Note that - _NDLT_ must be provided as a floating point number, with decimal point.

_DELTMX_          upper limit for time step size in seconds (default is infinite)

_ELST_               The name of an element to be tracked during time-stepping and its key thermophysical parameters will be written out in the log file. For the formatted input, only an element name with 5 characters is allowed.

_GF_                   magnitude (m/sec2) of the gravitational acceleration vector. Blank or zero gives "no gravity" calculation.

_REDLT_            factor by which time step is reduced in case of convergence failure or other problems (default is 4).

_SCALE_            scale factor to change the size of the mesh (default = 1.0).

Record **PARAM.2.1, 2.2**, etc. &#x20;

Free format for as more as 20 parameters, or Format (20E10.4)

&#x20;                      (DLT(I), I = 1, -_NDLT_)

_DLT(I)_             Length (in seconds) of time step I.

&#x20;                      This set of records is optional for _DELTEN_ = - _NDLT_, a negative integer. Input up to 100 time-step data. Multiple-line input is allowed, but each line inputs at least 1 data and at most 20 data.  If the number of simulated time steps exceeds the number of _DLT(I)_, the simulation will continue with time steps determined by automatic time step control (_MOP(16)_).

Record **PARAM.3**

Free format for 11 parameters, Format (11E10.4)

&#x20;           RE1, RE2, U, WUP, WNR, DFAC, FOR, AMRES, prvCR1, prvCr2, prvCR3

_RE1_                 convergence criterion for relative error, see Appendix B (default= 10-5).

_RE2_                 convergence criterion for absolute error, see Appendix B (default= 1).

_U_                     (void).

_WUP_               upstream weighting factor for mobilities and enthalpies at interfaces (default = 1.0 is recommended). 0 ≤ _WUP_ ≤ 1.

_WNR_               weighting factor for increments in Newton/Raphson - iteration (default = 1.0 is recommended). 0 < _WNR_ ≤ 1.

_DFAC_              increment factor for numerically computing derivatives (default value is _DFAC_ = 10-_k_/2, where _k_, evaluated internally, is the number of significant digits of the floating point processor used; for 64-bit arithmetic, _DFAC_ ≈ 10-8).

_FOR_                weighing factor determining the level of implicitness (default =1.0).

_AMRES_           Not be used in TOUGH4

_prvCR1_           convergence criterion for primary variable change, pressure (default=100.0).

_prvCR2_           convergence criterion for primary variable change, saturation, or mass fraction (default=0.001).

&#x20;_prvCR3_          convergence criterion for primary variable change, temperature (default=0.1).

Record **PARAM.4**        (optional) introduces the system phase-state index for the default primary variable set inputted through PARAM.5.  It is important only when the program cannot figure out its phase state through the primary variables. &#x20;

&#x20;                       Free format for 1 parameter, or Format (1I2)

&#x20;                       DefaultStateIndex       phase state index, can be found from tables in [Process Modeling](../../process-modeling/).&#x20;

Record **PARAM.5**        introduces a set of primary variables which are used as default initial conditions for all grid blocks that are not assigned by means of data blocks INDOM or INCON.

&#x20;                       Free format for as more as 20 parameters, or Format (4E20.13)

&#x20;                       DEP(I)_, I = 1, NumPriV_

The number of primary variables, _NumPriv_, is determined by the mass and energy component number of the flow system. If TOUGH3 initial condition is used as input, the _NumPriv_ equals _NKIN_+1. _NKIN_ is given in data block MULTI for special assignments. For formatted input, when more than four primary variables are used, more than one line (record) must be provided. Different sets of primary variables are in use for different EOS modules; see the description of [EOS modules](../../process-modeling/).                     &#x20;

If the phase state index has not been inputted with record PARAM.4, user can introduce it by inserting -DefaultStateIndex\*10 into any location of this record.  TOUGH4 will understand that it is for the DefaultStateIndex, if the data is less or equal -10.         &#x20;

**Used in**: All EOS modules

**Example**:   &#x20;

_PARAM_

_9,   2,    3000,     ,1000,    1,     0\*3,          3,        0\*8,     2,  ,  4_  &#x20;

_// ,     ,  MCYC,    ,MCYPR,  , MOP(2-4),  , MOP(6-13), , , MOP(16)_

_0.0, 27000.0,  -1.,  2000.,  , 9.8060          //TSTART, TIMAX, DELTEN, DELTMX,  , GF_

_20.                                                                    //DLT(1)_

_1.E-5,  1.E00, , , , 1.e-06,  ,  , 1000, 0.01, 0.1      // RE1, RE2,  ,  ,  , DFAC,  ,  , prvCR1, prvCr2, prvCR3_                 &#x20;

_2                                                                       //  phase state index._    &#x20;

_1.0133e5, 0.00, 0.0, 22.0                            //  default initial conditions._

The lase two lines can also be combined into one line:

_1.0133e5, 0.00, 0.0, 22.0, -20.0_   &#x20;
