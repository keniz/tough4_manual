# Problem 1-Multiphase and Nonisothermal Processes in a System with Variable Salinity (rf1)

This problem is from sample problem (rf1) in TOUGH3/EOS7 user manual. The problem, involving nonisothermal flow of variably saline brine and air, is not designed with an actual “real life” flow problem in mind; rather, the purpose is to demonstrate the use of a variety of thermodynamic conditions and generation options with EOS7 for the case of single gas (AIR) which is compatible to TOUG3/EOS7.

The model mesh is a three-dimensional 5x5x2 X-Y-Z regular mesh. Data block MODDE specifies InitCType  a value of "EOS7" which indicates that the model will use input file from TOUGH3/EOS7 and retain the same definition for the model (single gas component-air, with brine). MULTI is optional in TOUGH4 input. If MULTI exists, it must be no conflict with MODDE. The data block SELEC gives IE(402)=1 to force selecting constant HC (=1.0e-10) for air solubility calculation, using the same approach as TOUGH3/EOS7 for producing comparable results.  TOUGH4/EOS7 uses a sophisticated gas solubility model as default approach. &#x20;







&#x20;

&#x20;           Default initial conditions specified in the last record of data block PARAM are: pressure _P_ = 105 Pa, brine mass fraction _Xb_ = 0.5, air mass fraction _X_ = 0.0, and temperature _T_ = 25 ˚C. Various different initial conditions are chosen for portions of the flow domain in data block INCON. In the top layer, the first row of grid blocks (A11 1 through A11 5) has _Xb_ = 0.0, corresponding to single-phase water without salinity; the middle row (A13 1 through A13 5) has _Xb_ = 0.0, _X_ = 0.99, corresponding to single-phase gas conditions; the last row (A15 1 through A15 5) is initialized with _Xb_ = 1.0, corresponding to pure brine. In the bottom layer, two-phase conditions with 50 % gas saturation and different salinities are prescribed for the middle row (grid blocks A23 1 through A23 5). In blocks A23 1 and A23 2 the aqueous phase is pure water, in A23 3 it has 50 % brine mass fraction, and in A23 4 and A23 5 it is 100 % brine.

&#x20;

&#x20;           Generation options (data block GENER) include a well on deliverability in the upper left corner of the grid (A11 1), brine injection (COM2) in the upper right hand corner (A11 5), water injection (COM1) in the lower right hand corner (A25 5), heat generation in the center block of the lower layer (A23 3), and air injection (COM3) in the lower left corner (A25J1). Brine enthalpy is 106 J/kg, corresponding to a temperature of approximately 233 ˚C, while enthalpy of injected water, 3x105 J/kg, corresponds to a temperature of approximately 72 ˚C. Air is injected at a lower rate (10-4 kg/s) and enthalpy (2x105 J/kg). Air specific heat at constant pressure is approximately 1010 J/kg ˚C (Vargaftik, 1975), so that this enthalpy corresponds to a temperature of approximately 198 ˚C.



