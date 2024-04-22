# TOUGH4 Implementation

THOUGH was first developed about 40 years ago. However, its software architecture and data structure remain almost the same and without significant improvements. The rapid advancement of hardware, software, and computing platforms has made it challenging for TOUGH to fully harness the capabilities of modern computer technology. Despite the development of numerous process modeling modules, a lack of consistency and occasional overlap between these modules persists, and additional modules for different gas and gas mixtures are still highly expected. In addition, sharing modeling functionalities among different EOS (equation of state) modules remains a complex endeavor.

TOUGH4 re-engineers and expands TOUGH into a more general simulator by taking advantage of using the hybrid parallel computing hardware and using well-known third-party software libraries. TOUGH4 V1.0 has a completely modular structure, follows the tenets of Object-Oriented Programming (OOP), employs hybrid task based and data based parallel parallelism, and uses the standard data storage format for linear equation systems. It is designed with excellent extensibility for future development and great flexibility for adding any new process modeling capabilities. Besides inheriting all the user features from TOUGH3, it also adds many new features. The new simulator allows you to accommodate any number of EOS modules into a single executable. TOUGH4 simulations can be run in parallel with MPI, OPENMP, GPU or combination of any of them based on the computer hardware used and user preferences. The new version of the code is developed about 90% in Fortran and 10% in C++.

TOUGH4 retains all process modeling functionalities of TOUGH3, but it has completely reorganized the EOS modules. Most modules still use the same name, even though their modeling capabilities have significantly changed. The most important changes include: (1) EOS1 allowing water in supercritical conditions; (2) A new module named EO6 for any user specified gas simulation; (3) EOS7, EOS7R, EOS7C, EOS7CA are combined into a single EOS7 module; (4) ECO2N, ECO2M, ECO2N V2 are combined into a single ECO2 module; (5) EWASG are extended into allowing multiple gases and multiple salts. Several key process modeling capabilities have been generalized and can be used in any EOS modules, including (1) wellbore modeling; (2) simulation of decay chains, tracers, or solvents; (3) simulation of biodegradation reactions.  Table 1 lists all modules implemented in TOUGH4 and their modeling capabilities.&#x20;

Table 1. Fluid property modules for TOUGH4.

|              Module | Capabilities$$^{1,2}$$                                                                         |
| ------------------- | ---------------------------------------------------------------------------------------------- |
| EOS1                | water, water2, tracers $$^3$$, sub/supercritical condition                                     |
| EOS2                | water, CO2, tracers                                                                            |
| EOS3                | water, air, tracers                                                                            |
| EOS4                | water, air, with vapor pressure lowering, tracers                                              |
| EOS6                | water, user specified gas $$^5$$, tracers                                                      |
| EOS7                | water, brine, gases $$^4$$, tracers                                                            |
| EOS9                | variably-saturated isothermal flow according to Richards’ equation, tracers                    |
| EWASG               | water, salts, non-condensible gases$$^4$$                                                      |
| TMVOC               | water, water-soluble volatile organic chemicals, non-condensible gases, Tracers                |
| ECO2                | water, NaCl, CO2, tracers, including phase change among aqueous, supercritical and gaseous CO2 |

1\. Wellbore simulation is allowed for any EOS modules.

2\. Biodegradation reaction processes are allowed for any EOS modules.

3\. Tracers can be radionuclides or solvents with user designed parent-daughter relationship; can be in user specified phase. Tracer absorption can also be simulated. Handling the tracers may be slightly different in some EOS modules. The maximum number of tracers is 5.

4\. Maximum number of gases is 4

5\. Any gas with thermophysical properties provided by NIST Chemistry WebBook or other resources.

The present report provides a summary of the new features, discussions of the improvements in user features, data structure, software architecture, and process modeling capabilities over the previous versions. The mathematical models, numerical methods, module specific methods are discussed. This report also presents a quick start of using TOUGH4. It provides guides for compilation, installation, preparation of input files, and running simulations.  Discussion of the input file formatting is also presented, most of which remains compatible with TOUGH3.  To make this report self-contained for input file preparation, we include much of the material that was covered in the TOUGH3 user’s guide (Jung et al., 2018). Details of the mathematical models, numerical methods, module specific methods and testing examples can be found online.

TOUGH4 as the latest member of the codes, it is derived from many of these codes.  The following (Table 2) lists the main codes and key contributors.

Table 2. The most important codes that TOUGH4 is based on.

| Name of the Codes | Key Contributor     | What are the contributions to TOUGH4                                                                             |
| ----------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------- |
| TOUGH2            | Karstan Pruess      | General idea of the TOUGH simulation                                                                             |
| TOUGH3            | Yoojin Jung         | The user features (input/output and more)                                                                        |
| TOUGH+            | George Moridis      | Language style, data structure, and some user features                                                           |
| TOUGH2-MP         | Keni Zhang          | MPI parallelism                                                                                                  |
| EOS7C, EOS7CA     | Curt Odenburg       | EOS7                                                                                                             |
| TMVOC             | Karsten Pruess      | TMVOC                                                                                                            |
| ECO2N, ECO2M      | Karsten Pruess      | ECO2                                                                                                             |
| ECO2N V2.0        | Lehua Pan           | ECO2                                                                                                             |
| TMVOCBio          | Alfredo Battistelli | Biodegradation reactions                                                                                         |
| T2Well            | Lehuan Pan          | Wellbore simulation                                                                                              |
| ITOUGH2           | Stefan Finsterle    | Supercritical water simulation                                                                                   |
| TOUGH2/Hysteresis | Chris Doughty       | Hysteresis function for capillary pressure and relative permeability                                             |
| GPSFLOW           | Keni Zhang          | Hybrid parallel computing, data structure, new TOUGH software architecture, third-party linear solver interfaces |
| EWASG             | Alfredo Battistelli | EWASG                                                                                                            |
|  GasEOS           |  George Moridis     | Real Gas properties for gas mixture                                                                              |
|                   |                     |                                                                                                                  |
