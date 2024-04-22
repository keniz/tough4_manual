# ☑️ B: CAPILLARY PRESSURE FUNCTIONS

The new codes retain the same capillary pressure functions for two-phase or three-phase flow problems. Table lookup and interpolation using the user provided table as a new approach has been introduced in the TUGH4 for both relative permeability and capillary pressure function.

&#x20;The three-phase functions from TMVOC and ECO2 start at _ICP_ = 31. If one of the two-phase functions is chosen, the gas-NAPL (for TMVOC) or gaseous  $$CO_{2}$$-liquid  $$CO_{2}$$ (for ECO2) capillary pressure will be assumed to be zero. The notation used below is:&#x20;

$$P_{cgn}$$  = $$P_{l}$$  − $$P_{g}$$  = gas-NAPL capillary pressure for TMVOC, which is equivalent to $$P_{cgl}$$  = $$P_{l}$$  − $$P_{g}$$  = gaseous CO2-liquid CO2 capillary pressure for ECO2;&#x20;

$$P_{cgl}$$  = $$P_{l}$$  − $$P_{g}$$   = gas-aqueous capillary pressure for TMVOC, which is equivalent to $$P_{cga}$$  = $$P_{l}$$  − $$P_{g}$$   = gaseous CO2-aqueous capillary pressure for ECO2. It should be noted that _Pcnl_ is given by $$P_{cnl}$$  = $$P_{cgl}$$  − $$P_{cgn}$$   for TMVOC,&#x20;

and similarly  $$P_{cla}$$  = $$P_{cga}$$  − $$P_{cgl}$$   for ECO2.  $$S_{l}$$,  $$S_{g}$$, and  $$S_{n}$$ are the saturations of aqueous, gas (or gaseous  $$CO_{2}$$) and NAPL (or liquid  $$CO_{2}$$) phases, respectively.
