# Linear Solvers

TOUGH4 uses standard distributed CSR format matrix for storage of linear equation systems generated by the Newton-Raphson iteration. This provides great flexibility for calling any third-party linear solvers which use the standard CSR or BSR format matrix as input (A function for transforming CSR to BSR format is provided in the code).  TOUGH4 includes interface with several well-known solver packages including AMGCL, VIENNACL, FASP, PETSC, TRILINOS, AMGX and ROCALUTION. The original serial linear solver of TOUGH code has become obsolete as it does not provide any advantage for modern computing hardware. In TOUGH4, AMGCL (Demidov, 2019) was designed as the default linear solver.  AMGCL supports OPENMP, MPI and GPU parallel computing and allows the use of efficient AMG-CPR preconditioner. All the other linear equation solving packages have their own advantages. Table 3 summarizes the advantages and disadvantages of different packages.&#x20;

Table 3  Comparison of linear solver packages

<table><thead><tr><th width="168">Solver package</th><th width="274">Advantages</th><th>Disadvantages</th></tr></thead><tbody><tr><td>AMGCL</td><td>Include CPR preconditioner, support OPENMP, MPI and GPU parallel computing.</td><td>ILU is only available using OPENMP. MPI parallel computing is not very efficient.</td></tr><tr><td>VIENNACL</td><td>Allow use iterative solvers on both AMD and Nvidia GPU.</td><td>Only allow single GPU, no MPI.</td></tr><tr><td>FASP</td><td>Support Fast Auxiliary Space Preconditioning, support OPENMP.</td><td>Do not support MPI and GPU.</td></tr><tr><td>PETSC</td><td>Allow using many external packages, Include ILU, Jacobi, additive Schwarz preconditioner, allow user to build CPR preconditioner. MPI parallel computing is very efficient. </td><td>No or very limit support to hybrid parallel computing, limit support to GPU, no parallel ILU.</td></tr><tr><td>TRILINOS</td><td>Include ILU, Jacobi, additive Schwarz, and AMG, sometime better performance than PETSC.</td><td>No CPR preconditioner, difficult to compile on WINDOWS PC.</td></tr><tr><td>AMGX</td><td>Allow multiple GPUs.</td><td>For Nvidia GPU only.</td></tr><tr><td>ROCALUTION</td><td>Allow multiple GPUs, support OPENCL for different type of GPUs.</td><td>Limit efficient preconditioner.</td></tr></tbody></table>

TOUGH4 offers the option to link selected solver packages (except the default AMGCL package which is always included). Selection of the solver package, solving method, preconditioner, and input of other computing parameters are through keyword "[SOLVR](../preparation-of-model-input/keywords-and-input-data/solvr.md)".