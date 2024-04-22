# Running the Executable for Simulations

TOUGH4 can be run in many ways for different computing platforms. It allows you to provide some key parameters through command line. These parameters have the highest priority, which will override the default values, or the values input through the input files (most of these parameters can also be inputted through the keywork “MODDE”).  These parameters include:

\-t _n_:   n is number of threads/cores that will be used for the OPENMP parallel computing. If it is not provided, 4 threads or the maximum available threads (if less than 4) will be used.

\-f _filename_: The main input file name of the model. If not present, the default name “INFILE” will be used.

\-e _EOS\_name_: Select the EOS module for current simulation. It can be any one of the modules that have been compiled and included in the executable. If only one module is included in the executable, the default module will be the included module. The following modules are available in current version: 1-EOS1, 2-EOS2, 3-EOS3, 4-EOS4, 6-EOS6, 7-EOS7, 9-EOS9, 10-ECO2, 11-TMVOC, 12-EWASG.

\-i _TOUGH3\_module\_name_: Specify the type of module related data of the input file (for reading initial condition data and some module specific data). If not present, the default initial condition data for selected module will be applied.

\-g _true/false_: If the parameter is given a “true” or a non-zero value, the GPU linear solver will be used for solving linear equations (effect only when the GPU solvers has been included in the executable). The default value is “false”.

\-n true/false: whether current simulation is non-isothermal. If “true” or non-zero value, the model will run a non-isothermal simulation.

\-b _true/false_: If the parameter is given a “true” or a non-zero value, current simulation will include brine (EOS7), salt (ECO2), or second water (EOS1). Otherwise, these components will not be included in the model.

\-h or -H: Print the help messages, no simulation.

Following are several examples for running a simulation:

·         _tough4_

Run tough4 with default 4-thread parallel computing, the module to be run and other running parameters are given by the default values or reading from the section of keyword “MODDE“ in the main input file.

·         _tough4 –t 8 –e EOS3_

Run the EOS3 module with 8 thread parallel computing.

·         _mpiexec –n 2 tough4 –t 4 –e EOS7 –i eos7c_

Run the EOS7 module with eos7c input files using 2 MPI tasks and each task using 4 threads for hybrid parallel computing.

·         _tough4 –t 4 –e eco2 –i eco2m –g true -b 0_

Run the ECO2 module with eco2m input files using 4 threads for the parallel computing and 1 GPU for solving linear equations. The salt component is not included in the simulation.

Users should determine the best way to run their simulations based on the computer system they are using and the model size. In general, a small model using OPENMP gets better performance than using MPI. For large models, MPI may have better performance. Combinations for the OPENMP and MPI hybrid parallel computing may get the best performance.  GPU can perform well only for large models.  &#x20;
