# Parallel computing schemes

TOUGH4 uses the domain decomposition method together with OPENMP for hybrid parallel computing simulations. The hybrid parallelization was implemented through a three-tier parallel computing scheme. The first tier involves coarse-grained task-driven parallelization through domain decomposition, with each computational node or CPU serving as the basic unit. This is done by using METIS (ref.) for modelling domain partition to achieve the balance of computational tasks, memory requirement and communication volume among the participating CPUs. The second tier focuses on parallelization of the shared memory computational cores, which does not require computing task distribution; workload distribution among the cores is managed through multi-threading. This also ensures thread-safe in OPENMP multi-thread parallel computing, which is implemented by using a large loop for the assembly of a Jacobian matrix and EOS computation. The third tier utilizes data-driven parallelization, specifically GPU-based parallel computing. The GPU parallelization is for solving linear equations only and is implemented through using GPU supported third-party linear solvers.

The three-tier parallel computing scheme offers flexibility in utilizing any combination of the tiers:

(1)   using only the first tier, treating each computational core as a coarse-grained parallelization unit.

(2)   employing only the second tier without domain decomposition, suitable for small-scale simulation computations using a single CPU (multi-core, OPENMP multi-threading).

(3)   utilizing only the second and third tiers for single-GPU parallelization.

(4)   using a combination of the first and third tiers, or combination of all the three tiers.&#x20;

The first-tier parallelization is achieved through MPI for distributed or shared-memory CPU computer systems, while a hybrid approach combining MPI, OPENMP, and CUDA/OPENCL facilitates mixed distributed, shared-memory, and GPU parallel computing, accommodating three parallelization schemes simultaneously. An advanced local and global communication scheme was designed for the first-tier parallelization. In the hybrid parallelization scheme, domain decomposition assigns each computational unit (comprising a few computational cores, CPUs, GPUs, or a supercomputer node) responsibility for computing a subdomain of a model. Although the computations within each subdomain are independent, coordination between computational units is achieved through MPI communication to ensure the simulation runs as a coherent whole. All computational cores within each unit share memory space, collectively performing calculations within a subdomain. Solving linear equations, one of the most time-consuming portions, can be efficiently handled by GPUs. Figure 9 shows two typical parallel computing schemes.&#x20;

<figure><img src="../.gitbook/assets/try2 (1).jpeg" alt=""><figcaption><p>Figure 9. Typical Parallel computing schemes for core computations in TOUGH4</p></figcaption></figure>

Our empirical findings indicate that in scenarios without GPU involvement and with good inter-unit communication speeds, optimal results are achieved using pure MPI-based first-tier parallelization, albeit with higher memory requirements. In practical applications, consideration of the memory architecture of multi-core CPUs and supercomputer nodes is crucial in selecting the most suitable among the three parallelization schemes (hybrid, distributed-, or shared- memory) to achieve optimal parallel computing performance.
