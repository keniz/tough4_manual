# SOLVR

**SOLVR**            (optional) introduces a data block with parameters for linear equation solvers. For the PETSc solvers, other options could be specified through the PETSc (.petscrc) option files.

Record **SOLVR.1**

Free format for 6 parameters, or Format (I1, A4, A5, 2E10.4)

&#x20;             MatrixSolver, SolvingMethod, PCM, RITMAX, CLOSUR, MaxNumIter

_MatrixSolver_       Selection of linear solver library.

&#x20;                            1:  AMGCL

&#x20;                            2:  PETSC

&#x20;                            3:  FASP

&#x20;                            4:  VIENNACL

&#x20;                            5:  TRILINOS

&#x20;                             6:  AMGX

&#x20;                             7:   ROCALUTION

&#x20;                             8:  TOUGH series solver (not used in current version)

_SolvingMethod_  Linear equation solving method.

&#x20;                             GM: GMRES

&#x20;                             BC: BiCGSTAB

_PCM_                  Preconditioning method.

&#x20;                             JA:  JACOBI

&#x20;                             IL:  ILU

&#x20;                             CP: AMG-CPR (for AMGCL and FASP only)

&#x20;                             AS: Additive Schwarz&#x20;

&#x20;                             DC: Domain Decomposition

&#x20;                             AM: AMG

&#x20;                             DR:  CPR-DRS (For AMGCL only)

_RITMAX_               (not used).

_CLOSUR_               Convergence criterion for the iterations (1.e-12 ≤ CLOSUR ≤ 1. e-6; default is 1.e-6).

_MaxNumIter_         Maximum number of iterations in solving linear equations.

**Used in**: All EOS modules

**Example**:

_SOLVR_

_AMGCL, GM, CPR,  ,1.0e-6, 200_
