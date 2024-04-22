# BIODG

**BIODG**           input data block introducing parameters needed to simulate the biodegradation processes.

Record **BIODG.1**

&#x20;                       Free format for 7 parameters, or Format (I5,I5,E10.4,10X,4E10.4)

&#x20;                       IMONOD, ICFLAG, BFAC, SW1, SW2, WEA, WSUB

_IMONOD_          selects between multiplicative and minimum Monod model for the substrate degradation rate equation.

&#x20;        0 : multiplicative Monod model (default).

&#x20;        \>0 : minimum Monod model.

_ICFLAG_          selects how to consider the competitive and Haldane inhibition terms in the Monod model.

&#x20;       \=0: competitive and Haldane inhibition factors are applied to all Monod terms in the substrate degradation rate equation, including the electron acceptor and nutrients terms as in the BIOMOC code formulation (default).

&#x20;       \>0: competitive and Haldane inhibition factors are applied only to the substrate Monod term, as in conventional formulations of cometabolic degradation processes modelled using competitive inhibition effects.

_BFAC_               reduction factor criterion for local Newton-Raphson iteration to reduce substrate residual. Nonlinearity of the reaction is handled by local Newton-Raphson iteration for the primary substrate.  _BFAC_ is the factor by which the residual must be reduced before convergence.

_SW1_                 lower limit of aqueous phase saturation considered in the saturation inhibition function (if =0, the default value 0.02 will be applied.).

_SW2_                 upper limit of aqueous phase saturation considered in the saturation inhibition function (SW1 < SW2 ≤ 1).

_WEA_                 weighting factor for the linear interpolation of electron acceptor and nutrients concentrations to be used in the substrate degradation rate equation (0 < WEA ≤ 1). Default value is WEA = 0.5. WEA = 1 corresponds to using the concentration evaluated at the end of the time step.

_WSUB_               weighting factor for the linear interpolation of substrate concentration to be used in the substrate degradation rate equation (0 < WSUB ≤ 1). Default value is WSUB = 0.5. WSUB=1 corresponds to using the concentration evaluated at the end of the time step.

Record **BIODG.2**

&#x20;                       Free format for 1 parameter, or Format (I5)

&#x20;                       NPROC

_NPROC_            number of biodegradation processes in the simulation (NPROC ≤ 20).

Record **BIODG.3**

&#x20;                       Free format for 8 parameters, or Format (2(5X, I5), 2E10.4, 3(5X, I5), E10.4)                      &#x20;

NSPROC(IP), IBIO(IP), AMUMAX(IP), YIELD(IP), NCOMP(IP), NNC(IP), NHAL(IP), ENTB(IP)

_NSPROC(IP)_   number of mass components controlling the substrate degradation rate in process IP.

_IBIO(IP)_          index of microbial population involved in process IP.

&#x20;_AMUMAX(IP)_         maximum specific substrate degradation rate in process IP (kg substrate/ (s kg biomass) ).

_YIELD(IP)_        yield coefficient for the growth of biomass due to the degradation of unit mass of substrate in process IP (kg biomass / kg substrate).

_NCOMP(IP)_     number of mass components responsible for competitive inhibition in process IP.

_NNC(IP)_          number of mass components responsible for non-competitive inhibition in process IP.

_NHAL(IP)_          number of mass components responsible for Haldane inhibition in process IP.

_ENTB(IP)_          heat of reaction for the degradation of substrate in process IP (J/kg substrate).

Record **BIODG.4**

&#x20;                       Free format for as more as 12 parameters, or Format ( 6(5X, I5, E10.4) )

&#x20;                       KSPROC(IP,NC), AKS(IP,NC) ; NC=1, NSPROC(IP)

_KSPROC(IP,NC)_     index of mass component # NC controlling the substrate degradation rate in process IP. By convention, the first (NC=1) must refer to the primary substrate of process IP.

_AKS(IP,NC)_     half saturation constant of mass component # NC in the Monod term of substrate degradation rate in process IP (kg substrate / kg aqueous phase). If specified, must be >0.

Record **BIODG.5**

&#x20;                       Free format for as more as 12 parameters, or Format ( 6(5X, I5, E10.4) )

&#x20;                       KSCOMP(IP,NC), AKCOMP(IP,NC) ; NC=1, NCOMP(IP)

_KSCOMP(IP,NC)_     index of mass component # NC responsible for competitive inhibition in process IP.

_AKCOMP(IP,NC)_     competitive inhibition coefficient for mass component # NC in process IP (kg solute / kg aqueous phase).

Record **BIODG.6**

&#x20;                       Free format for as more as 12 parameters, or Format ( 6(5X, I5, E10.4) )

&#x20;                       KSNC(IP,NC), AKNC(IP,NC) ; NC=1, NNC(IP)

_KSNC(IP,NC)_          index of mass component # NC responsible for non-competitive inhibition in process IP.

_AKNC(IP,NC)_          non-competitive inhibition coefficient for mass component # NC in process IP (kg solute / kg aqueous phase).

Record **BIODG.7**

&#x20;                       Free format for as more as 12 parameters, or Format ( 6(5X, I5, E10.4) )

&#x20;                       KSHAL(IP,NC), AKHAL(IP,NC) ; NC=1, NHAL(IP)

_KSHAL(IP,NC)_       index of mass component # NC responsible for Haldane inhibition in process IP.

_AKHAL(IP,NC)_       Haldane inhibition coefficient for mass component # NC in process IP (kg solute /kg aqueous phase).

Record **BIODG.8**

&#x20;                       Free format for as more as 20 parameters, or Format (8E10.4)

&#x20;                       UPTAKE(IP,L) ; L=1,NumCom

_UPTAKE(IP,L)_       uptake coefficient of component # L in process IP with respect to 1 mole of degraded primary substrate (mole component / mole substrate).

Repeat records BIODG.3 through BIODG.8 for a total of NPROC (up to 20) different biodegradation processes (IP= 1, NPROC).

Record **BIODG.9**

&#x20;                       Free format for 2 parameters, or Format (2I5)

&#x20;                       NPOP, IBFLAG

_NPOP_               number of microbial populations (NPOP ≤ 20).

_IBFLAG_          specifies if initial conditions for biomass concentration are supplied through input blocks INDOM, INCON, or through an INCON file.

0: constant biomass concentrations are given as initial conditions through block BIODG.10.

\>0: variable biomass concentrations are supplied as initial conditions through blocks INDOM, INCON or through an INCON file.

Record **BIODG.10**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       BAI(IB), BA0(IB), TMAX(IB), DEATH(IB), AKBIO(IB)

_BAI(IB)_          initial concentration (valid for the entire simulation grid) in the aqueous phase of microbial population # IB (kg biomass / kg aqueous phase).

_BA0(IB)_          minimum concentration in the aqueous phase of microbial population # IB enforced during the simulation (kg biomass / kg aqueous phase).

_TMAX(IB)_       maximum temperature for the calculation of temperature inhibition function in the substrate degradation rate equation (°C).

_DEATH(IB)_      death rate constant, or maintenance constant, for the microbial population # IB (s-1).

_AKBIO(IB)_        inhibition constant for biomass growth of microbial population # IB (kg biomass kg aqueous phase).

Repeat record BIODG.10 for a total of NPOP (up to 20) different microbial populations (IB= 1, NPOP).

**Used in**: All EOS modules

**Example**:

_BIODG_----1----_----2----_----3----_----4----_----5----_----6----_----7----\*----8

_0,  1.e-10,  ,  0.0 ,  .2,  0.9,  0.9_                          //BIODG.1

_2_                                                                              //BIODG.2&#x20;

_2, 1, 1.2732e-5, 1.0, 0, 0, 0, 0.0_                         //BIODG.3 for process 1&#x20;

_4, 2.e-6, 2, 1.e-6_                                                 //BIODG.4 for process 1&#x20;

_0_                                                                            //BIODG.5 for process 1&#x20;

_0_                                                                          //BIODG.6 for process 1&#x20;

_0_                                                                         //BIODG.7 for process 1&#x20;

_-4.0, 9.0, 0.0, 1.0_                                               //BIODG.8 for process 1    &#x20;

_2, 1, 1.1574e-5, 0.8, 0, 0, 0, 0.0_                      //BIODG.3 for process 2&#x20;

_3, 1.e-6, 2, 0.5e-6_                                              //BIODG.4 for process 2&#x20;

_0_                                                                          //BIODG.5 for process 2

_0_                                                                           //BIODG.6 for process 2&#x20;

_0_                                                                           //BIODG.7 for process 2&#x20;

_-3.0, 7.5, 1.0,  0.0_                                              //BIODG.8 for process 2              &#x20;

_1_                                                                           // BIODG.9      &#x20;

_1.530e-6, 1.00e-6, 40.,  2.3148e-7, 0.0_       //BIODG.10
