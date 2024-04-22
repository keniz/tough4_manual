# 2️⃣ WHAT IS NEW IN TOUGH4

TOUGH4 fully inherits process modeling capacities from TOUGH3 and retains the backward compatibility for input/output formats. Significant improvements have been made in software architecture, data structure, parallel computing, and EOS process modeling. The key new features of TOUGH4 are summarized as follows:

·         Software architecture

TOUGH4 rewrote the TOUGH from the first line of the source codes with the concept of Object-Oriented Programming (OOP) and hybrid parallelism. It was designed for both tasks driven, and data driven parallel computing. With these concepts, significant changes have been made for the key components of the simulator, including Jacobian matrix setup and EOS calculation. The new software architecture improves efficiency in memory usage, computing performance, software readability and extensibility, and reuse of the codes. For example, the previous versions of TOUGH needs calculation of secondary variables for all the primary variables and shifted primary variables before the construction of Jacobian matrix and solving the equation systems. This approach requires storage of secondary variables for all sets of primary variables and shifted primary variables (array PAR in TOUGH3), which may require huge memory space when a model has many elements or/and more mass components. It is also not a favorite for data-driven parallelism. In TOUGH4, the procedure for calculation of secondary variables and setup Jacobian matrix is organized in a big loop for performing the calculation element by element.   The new approach will significantly reduce memory requirements for storage of secondary variables (No need storage of the secondary variables calculated from the sets of shifted primary variables), and the new approach is ready for efficient data-driven parallel computing.

·         Data structure

Many procedures and functions with data encapsulation are designed as modules. This approach significantly improves the reuse of the data and functions as objects in different EOS modules and can greatly benefit the future developments of new modules. In TOUGH4, the user defined structures for data have been widely used. The use of structure-type data significantly improves the management of data and software readability. In the new version, the matrix and right-hand-side vector of the linear equation system obtained from Jacobian matrix setup are stored in a standard distributed CSR (Compressed Sparse Row) format. By using this format, the third-party linear solver libraries can be called easily.&#x20;

·         Hybrid parallel computing

TOUGH4 uses domain decomposition for task based parallel computing. A large granularity parallelism is implemented through MPI and uses Metis for the model mesh partitioning. Inside each subdomain, OPENMP is used for the implementation of data-driven parallel computing. For solving linear equations, parallel computations with MPI, OPENMP, or GPUs are allowed through well-known third-party linear solvers. GPU with both OPENCL and CUDA is supported by the new version of TOUGH. Hybrid parallel computing with the combination of MPI, OPENMP and GPU can be used to achieve the best performance for different hardware.

·         Consolidation of EOS modules

Some EOS modules are consolidated into one module. The new ECO2 covers the original three modules of ECO2N, ECO2M and ECO2N V2.0 in TOUGH3. ECO2 is for three-phase simulation, but retains the flexibility for users to run simulation in two-phase (compatible with ECO2N, ECO2N V2.0).  The new EOS7 module covers the original four modules of EOS7, EOS7R, EOS7C, and EOS7CA in TOUGH3, and extends to the simulation of as many as 4 gas mixtures.

·         Simulation of decay chain, biodegradation, and absorption for tracers

As many as five tracers can be simulated with any EOS module. These tracers are allowed in a user specified phase. They can be treated as first-order decay/biodegradation, or absorption. For the decay chain, complex parent-daughter relation can be designed by user, and tracers allow to have multiple parents and daughters. Tracers are treated in slightly different ways in some EOS modules. For example, EOS7 allows tracers partitioning among both aqueous and gaseous phase, TMVOC allows tracers in aqueous phase only, and EWASG treats the tracers as salts, and allows the salts to precipitate or dissolve.  The “salts” can be in aqueous or/and solid phase.

·         Primary variables

In order to get better simulation performance, some EOS modules use different primary variables from the previous version of TOUGH. EOS3 and EOS4 allow using different sets of primary variables based on user’s selection. TOUGH4 has the flexibility in the number of equations to be solved for each EOS module. The number of primary variables (equations) are determined based on the number of tracers, gases, and other options in the run-time.

·         EOS1 Module

In TOUGH4, EOS1 is extended to simulate supercritical water conditions. The temperature and pressure are allowed to be as high as 1000$$^oC$$and 1000MPa.  The module retains two water components but allows existence of tracers (as many as 5).  Vapor pressure lowering from capillary and adsorption effects has been included in the module.

·         ECO2 module

The ECO2 module was designed for simulation of CO2 in saline aquifers at the temperature 10-300$$^oC$$ with pressures as high as 600 bar. The flow system can be in three phases (aqueous, supercritical or/and gas phases). A CO2 property module was developed which can be flexibly used by any EOS modules. The CO2 property calculation by analytical solutions of Altunin (1975) has been implemented in the CO2 property module, which means the CO2TAB is no longer a necessary now and also the code is more flexible for different range temperature and pressure simulation.  In the new codes, the component NACL is optional (less equation to be solved).  &#x20;

·         EOS6 module

A completely new module, EOS6, was developed for simulation of two-phase, non-isotheral flow of a single gas and water in subsurface. The gas can be any gas listed in the NIST database. The thermophysical properties of the fluid are directly interpolated from the NIST database or provided by the user. The solubility, which has not been provided by NIST database, can be determined in four options: user inputted Herry’s constant, calculation with CRAMER (1982), calculation with D'AMORE AND TRUESDELL (1988), or interpolation from a table provided through a data file with temperature dependent Herry’s constants.

·         EOS7 module

EOS7 was designed for the simulation of subsurface flow consisting of as more as 4 gas mixtures, brine, water and tracers in a large range of temperature and pressure.  The four gases can be any combination of the lists of 13 gases in the gas library implemented in the module of real-gas properties. The gas components are treated as real gases and use the cubic equation of state to solve thermophysical properties. A new solubility calculation method was developed to handle the solubility of mixed gases and avoid the convergence problem of gas solubility solution approach in TOUGH3/EOS7C. The brine and tracers are all optional.

·         EWASG

EWASG was extended to the simulation for multiple gases and multiple salts. In contrast to EOS7, it describes aqueous fluid of variable salinity not as a mixture of water and brine, but as a mixture of water and salts. The mixture of gas components is treated as real gases and uses the cubic equation of state to solve thermophysical properties. The gas solubility model was improved by adopting the accurate chemical equilibrium approach as originally implemented in EOS7C for calculation of aqueous phase gas solubilities. The salts are not only the NACL, but also any other salts.  In the current implementation, a simplified salt solubility model is used, which describes solubility of any salt as a linear function to NACL solubility.&#x20;

·         Wellbore simulation

Wellbore simulation was developed based on the T2WELL, which uses the extended drift-flux model (DFM) for solution of transient (momentum balance) mixture velocity. The fluxes between two neighboring wellbore elements are calculated using the mixture velocity. The energy balance takes into account of the fluid internal energy, heat advection and conduction, kinetic energy, potential energy, and lateral wellbore heat loss/gain. The well flow is treated as a two-phase flow system. If the third phase exists, the third phase will be simplified as a portion of the gaseous phase. The wellbore simulation was implemented as a module and generalized for use in any EOS modules.

·         Modeling of Biodegradation reactions

The development of the modeling capability of biodegradation reaction processes is based on the TMVOCBio, which was implemented in the TOUGH3/TMVOC. The capability allows simulation of multiple biodegradation reactions mediated by different microbial populations or based on different redox reactions, thus involving different electron acceptors. It uses a general modified form of the Monod kinetic rate equation to simulate biodegradation reactions, which effectively simulates the uptake of a substrate while accounting for various limiting factors (i.e., the limitation by substrate, electron acceptor, or nutrients). As the limiting factors, biomass growth inhibition, toxicity effects, as well as competitive and non-competitive inhibition effects are included. The temperature and moisture dependence of biodegradation reactions is also considered. This modeling functionality is generalized for all EOS modules as long as the biodegradation reactions existing in the simulated flow system. &#x20;

·         Real-Gas properties

The general approach for calculation of real-gas properties remains its original implementation in TOUGH3. The real gas properties module has options for Peng-Robinson, Redlich-Kwong, or Soave-Redlich-Kwong equations of state to calculate gas mixture density, enthalpy departure, and viscosity. In TOUGH4, 5 more gas components (with a total of 13 gases) are included in the gas list for simulation. Some parameters for viscosity, solubility, enthalpy calculation, and binary interaction parameters (BIPs) were calibrated. Addition to the original approaches, the Quinones et al. (1984;1988) method was implemented for mixed gases viscosity calculations.

·         Linear solvers

As we are using the standard distributed CSR format for storage of the matrix and right-hand side vector of the linear equation system, it is easy to call the most well-known third-party linear solvers. A function for converting CSR to BCSR is included for solvers which may get additional efficiency by using BCSR. At this moment, interfaces to the following linear solver libraries have been developed:  AMGCL, PETSC, TRILINOS, FASP, VIENNAVCL, AMGX, and ROCALUTION. These solver libraries are among the most well-known linear solvers in the public domain.  The abundant solver selections allow TOUGH users to choose the best solver for their computer platform.  These solvers include CPR-AMG preconditioner (AMGCL and FASP), which is widely recognized by people in oil/gas reservoir simulation community as the best performance preconditioner, matured MPI parallel solvers (PETSC and TRILINOS), GPU solver on PC (VIENNACL), and multiple-GPU solvers (AMGX and ROCALUTION) on supercomputers for CUDA and OPENCL respectively.

·         Additional well production or injection types

Except the original types for the source/sink, the new version TOUGH support more options for well production or injection TYPE. The TYPE can be the component name, for example “CO2” means injection or production of CO2. Additional types include:  GAPP (produce gases with given bottomhole pressure), AQPP (produce aqueous phase fluid with given bottomhole pressure), OIPP (produce oil/non-aqueous phase fluid with given bottomhole pressure), GAPR(produce gas phase fluid with given production rate), AQPR(produce aqueous phase fluid with given production rate), OIPR (produce oil phase fluid with given production rate), GAIP (injection mix gases with given pressure), AQIP (injection mix aqueous fluid with given pressure), and OIIP (injection mix oil/non-aqueous phase fluid with given pressure)

·         Flexible Input formatting

The TOUGH4 accepts TOUGH3 input formats. However, it also allows the input data in free format with comma or semicolon as a “separator”. For example, TOUGH3 inputs 10 different type parameters in a text line with certain format. The new version will also input the same parameters without formatting but separating all the parameters by a “separator”. Users can use the old format or new style for different lines in the same input file. TOUGH4 will automatically identify the text lines with new style input.

·        Dynamic number of components

The number of equations per gridblock to be solved are dynamically adjusted based on the model setup at runtime. User can define the number of gases, number of tracers, whether existing of brine/water2, isothermal or non-isothermal condition. This guarantees the efficient use of computer memory and computing resources.

·        Dynamic build of the executable

The executable can be built based on the user’s preference, such as which and how many EOS modules are included, what linear solvers are linked, whether the executable supports MPI or OPENMP parallel computing, whether it supports GPU simulation and whether the METIS will be included.   With the OOP design, the new executable is allowed to contain any number of EOS modules. This means that a single executable can run for different EOS modules. &#x20;

·         Other features

Such as CO2 density correction for the cubic equation of state using the CO2 property module, optional selection of use absolute primary variable changes as the Newton iteration convergence criteria, run-time adjusting of key model computation parameters, allowing element or connection outputs in original mesh order or in the CPU sequence, flexible element name length (3-10 characters),  allowing use of table interpolation as the relative permeability and capillary pressure functions, and many others.
