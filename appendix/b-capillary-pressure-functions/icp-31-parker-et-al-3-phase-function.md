# ICP=31   Parker et al 3-phase function

_ICP_=31           Three-phase capillary functions from Parker et al. (1987).

&#x20;                       _m_ = 1 -1/_n_

$${\bar S_l} = ({S_l} - {S_m})/(1 - {S_m})$$

$${\bar S_n} = ({S_l} + {S_n} - {S_m})/(1 - {S_m})$$

$${P_{cgn}}\quad  = \quad  - \;\frac{{{\rho _l}g}}{{{\alpha _{gn}}}}\;{[{({\bar S_n})^{ - 1/m}} - 1]^{1/n}}$$

$${P_{cgl}} =  - \frac{{{\rho _l}g}}{{{\alpha _{nl}}}}{\left[ {{{\left( {{{\bar S}_l}} \right)}^{ - 1/m}} - 1} \right]^{1/n}} - \frac{{{\rho _l}g}}{{{\alpha _{gn}}}}{\left[ {{{\left( {{{\bar S}_n}} \right)}^{ - 1/m}} - 1} \right]^{1/n}}$$

where $$S_m$$ = _CP(1)_; _n_ = _CP(2)_; $$\alpha _{gn}$$ = _CP(3)_; $$\alpha _{nl}$$  = _CP(4)_.

These functions have been modified so that the capillary pressures remain finite at low aqueous saturations. This is done by calculating the slope of the capillary pressure functions at $${\bar S_l}$$ and $${\bar S_n}$$ = 0.1. If t $${\bar S_l}$$  or t $${\bar S_n}$$ is less than 0.1, the capillary pressures are calculated as linear functions in this region with slopes equal to those calculated at scaled saturations of 0.1.

