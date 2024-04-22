# Scope and Methodology

The TOUGH4 simulator remains most of the scope and methodology of original TOUGH. It is developed for applications involving subsurface flow problems. The simulator solves mass and energy balance equations that describe fluid and heat flow in general multiphase, multicomponent, and multidimensional systems. It fully accounts for the movement of gaseous, aqueous, and non-aqueous phases, the transport of latent and sensible heat, and the transition of components between the available phases, which may appear and disappear depending on the changing thermodynamic state of the system. Advective fluid flow in each phase occurs under pressure, viscous, and gravity forces according to the multiphase extension of Darcy's law, which includes relative permeability and capillary pressure effects. In addition, diffusive mass transport can occur in all phases. The code includes Klinkenberg effects in the gas phase and vapor pressure lowering due to capillary and phase adsorption effects. Heat flow occurs by conduction and convection, as well as radiative heat transfer according to the Stefan-Boltzmann equation. Local equilibrium of all phases is assumed to describe the thermodynamic conditions. TOUGH4 can simulate the injection or production of fluids and heat, and also includes different options for considering wellbore flow effects. Effects of sorption onto the solid grains, radionuclide transport, or biodegradation can be simulated as well for all EOS modules.

TOUGH4 uses an integral finite difference method (IFDM) for space discretization. The IFDM (Edwards, 1972; Narasimhan and Witherspoon, 1976) avoids any reference to a global system of coordinates, and thus offers the advantage of being applicable to regular or irregular discretizations in one, two, and three dimensions. The IFDM also makes it possible, by means of simple preprocessing of geometric data, to implement double-porosity, dual-permeability, or multiple interacting continua (MINC) methods for fractured media (Pruess and Narasimhan, 1982, 1985; Pruess, 1983). No particular price needs to be paid for this flexibility; indeed, for systems of regular grid blocks referring to a global coordinate system, the IFDM is completely equivalent to conventional finite differences. Time is discretized fully implicitly as a first-order backward finite difference. The implicit time-stepping and the 100% upstream weighting of flux terms at interfaces are necessary to avoid impractical time step limitations in flow problems involving phase (dis-)appearances, and to achieve unconditional stability (Peaceman, 1977). The resulting strongly coupled, nonlinear algebraic equations are solved simultaneously using Newton-Raphson iterations for each time step, which involves the calculation of a Jacobian matrix and the solution of a set of linear equations. Time steps are automatically adjusted during a simulation run, depending on the convergence rate of the iteration process. Newton-Raphson increment weighting can also be adjusted if the iterations oscillate.&#x20;

TOUGH4 can simulate various fluid mixtures by means of separate EOS modules, which internally calculate the thermophysical properties of specific fluid mixtures, e.g., fluid density, viscosity, and enthalpy. Due to this flexibility to handle a variety of flow systems, TOUGH4 can be used for diverse application areas, such as geothermal reservoir engineering, geological carbon sequestration, natural gas reservoirs, nuclear waste isolation, environmental assessment and remediation, and flow and transport in variably saturated media and aquifers, among other applications that involve nonisothermal multiphase flows.