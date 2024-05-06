# Problem 1 - Code Demonstration

This problem demonstrates various initialization options and phase transitions. A number of one- and two-element subproblems are simulated which are entirely independent of each other (no flow connections between subproblems), except that being run together they all must go through the same sequence of time steps. The standard method for initialization is used for “F   1”, “F   2”, and “F   5” in single-phase liquid conditions and for “F   3” in two-phase condition. “F   4” is initialized with two-phase type primary variables, but with temperature for the first primary variable. Data block OUTPU is used to select variables to print out, and data blocks FOFT and GOFT are used to generate time series for selected grid blocks and generation items that can be used for plotting.

Details of this example can be found in [EOS1 manual](https://drive.google.com/file/d/19jQ5UnMi8XPlm6PZp59NQr2p6D8Y55DZ/view?usp=drive\_link), sample 1 (eos1p1).

**Input files**

[INFILE](https://drive.google.com/file/d/1sno7WLy4xVnrnmgCvkkq6gzfy7FPn9cU/view?usp=sharing)

**Output Files**

[eosp1.zip](https://drive.google.com/file/d/1IM\_E4wumlMN0PcjvBKitBcIJ00lMCLpk/view?usp=sharing)
