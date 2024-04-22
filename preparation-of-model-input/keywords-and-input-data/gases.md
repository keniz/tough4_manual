# GASES

**GASES**          introduces gas parameters, For EOS6, EOS7, TMVOC and EWASG only.&#x20;

Record **GASES.1**

&#x20;                       Format (1I5) or free format

&#x20;                       NumGas

_NumGas_              Number of gases to be simulated, the maximum is 4 for EOS7 and EWASG, 1 for EOS6, and 8 for TMVOC.

Record **GASES.2**

&#x20;                       Free format for 14 parameters

&#x20;                       GasName, OCKM, ALAMM, AMWTM, SolCM, b(i) (i=0-8)

_GasName_         Name of the gas. It must be selected from following list: CH4, C2H6, C3H8, H2S, CO2, N2, O2, C2H5OH, H2, nC4H10, iC4H10 and AIR for module EOS7 and EWASG; CH4, C2H6, H2S, CO2, N2, O2, H2, AIR, NH3, C2H2, and C2H4 for TMVOC; and any name for EOS6.

_OCKM_              Gas carbon partition coefficient Koc,  $$m^3/kg$$ (not used in current version).

_ALAMM_           Decay constant for biodegradation, default value is 0.0. (Used by EOS6                                         only)

&#x20;_AMWTM_         Gas molecular weight, g/mole, for EOS6 only.

&#x20;_SolCM_             Gas solubility calculation method, for EOS6 only

&#x20;                                      \=0, constant HC (Default)

&#x20;                                      \=1, interpolation HC from table provided through data file by user.

&#x20;                                      \=2, use CRAMER (1982) or D'AMORE AND TRUESDELL (1988).

&#x20;                                      \=3, use Equation (8-3)

_b(i)_                    i=0-8, parameters for HC calculation when _SolCM=0,_ 2 or 3, for

&#x20;                                      EOS6 only.

Parameters for calculation of Henry's constant are inputted through the array _b(i)_. The following are the functions used for the calculation of _hc_:

(1)   _SolCM_=0

Default _hc=_ _1.0e-10. If b(0)>0.0, hc=b(0)\*1.0e-10._&#x20;

(2)   _SolCM_=1

See Appendix E for details.

_(3)   SolCM=2_

$$hc=\dfrac{1.0}{(b_1+b_2t+b_3t^2+b_4t^3+b_5t^4+b_6t^5+b_7t^6+b_8t^7)*101325}$$                                        (8-2)

_where_ $$b_i=b(i)$$&#x20;

_t_ is temperature in degrees Celsius (_°C_).

For special cases with _b(1) has_:

_b(1)=-1_: _hc=b(0)\*hc\_CH4_.

_b(1)=-2_: _hc=b(0)\*hc\_CO2_.

_b(1)=-3_: _hc=b(0)\*hc\_N2_.

_b(1)=-4_: _hc=b(0)\*hc\_O2_.

_b(1)=-5_: _hc=b(0)\*hc\_H2_.

_b(1)=-6_: _hc=b(0)\*hc\_AIR_.

&#x20;_hc\_CH4, hc\_CO2, hc\_N2, hc\_O2, hc\_H2,_ and _hc\_AIR_ are calculated internally using the equation (8-2) with parameters from literatures Cramer (1982) or Damore and Truesdell (1988).

_(4)   SolCM=3_

$$hc=10^{-6}*e^{-(b_1+b_2*tk+b_3/tk+b_4*log(tk))}$$                                                                                          (8-3)

_where bi=b(i)_

_tk_ is temperature in Kelvin.

For special cases with _b(1)<0_:

_b(1)=-1_: _hc=b(0)\*hc\_C2H6_.

_b(1)=-2_: _hc=b(0)\*hc\_C3H8_.

_b(1)=-3_: _hc=b(0)\*hc\_H2S_.

_b(1)=-4_: _hc=b(0)\*hc\_nC4H10_.

_b(1)=-5_: _hc=b(0)\*hc\_iC4H10_.

_hc\_C2H6, hc\_C3H8, hc\_H2S, hc\_N-C4H10,_ and _hc\_I-C4H10_ are calculated internally using the equation (8-3) with parameters from literatures Damore and Truesdell (1988).

For EOS7 and EWASG module, the gas name must be one of the gases implemented in the gas library (CH4, C2H6, C3H8, H2S, CO2, N2, O2, C2H5OH, H2, nC4H10, iC4H10, AIR). &#x20;

For TMVOC module, the gas name must be chosen among the 11 gases included in the internal data bank: CH4, C2H6, H2S, CO2, N2, O2, H2, AIR, NH3, C2H2, C2H4.

Repeat the record GASES.2 for _NumGas_ times for input of all the gases.

If  _InitCType_ in [MODDE.1](modde.md) is "EOS7", "EOS7R", "EOS7C", or "EOS7MG", default gases for the corresponding EOS modules will be used and the input for "GASES" can be neglected.&#x20;

**Used in**: EOS6, EOS7, TMVOC, EWASG

**Example**:

_GASES_

_2                                            //two gases are defined for current simulation_

_H2_

_CO2_
