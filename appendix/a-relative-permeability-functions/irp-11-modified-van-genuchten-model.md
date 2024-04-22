# IRP=11  Modified van Genuchten Model

_IRP_ = 11         Modified van Genuchten Model

A modified version of the van Genuchten model (Luckner et al., 1989) has been implemented to prevent the capillary pressure from decreasing towards negative infinity as the effective saturation approaches zero. The modified van Genuchten model is invoked by setting both _IRP_ and _ICP_ to 11.

$${k_{rl}} = S_{ekl}^\gamma  \cdot {S_{ekl}}^{(1 - \gamma )\eta } \cdot {\left[ {1 - {{\left( {1 - {S_{ekl}}^{(1 - \gamma )/m}} \right)}^m}} \right]^2}$$

$${k_{rg}} = \left\{ {\begin{array}{*{20}{c}} {{{\left( {1 - {S_{ekg}}} \right)}^\zeta }{{\left[ {1 - {S_{ekg}}^{1/m}} \right]}^{2m}}{\rm{     if RP(3) }} = {\rm{ 0}}}\\ {1 - {k_{rl}}{\rm{                                 if RP(3)}}{\rm{ }} \ne {\rm{ 0}}} \end{array}} \right.$$

where

$${S_{ekl}} = \frac{{{S_l} - {S_{lrk}}}}{{1 - {S_{lrk}}}}$$, $${S_{ekg}} = \frac{{{S_l}}}{{1 - {S_{gr}}}}$$

Parameters: _RP(1)_ = $${S_{lrk}}$$

if negative, $${S_{lrk}} = 0$$ for calculating _krg_, and absolute value is used for calculating _krl_

_RP(2)_ = $${S_{gr}}$$if negative, $${S_{gr}} = 0$$ for calculating _krl_, and absolute value is used for calculating _krg_

_RP(3)_ = flag to indicate which equation is used for _krg_

_RP(4)_ = $$\eta$$ (default = 1/2)

_RP(5)_ = $$\epsilon_k$$

use linear function between $${k_{rl}}({S_e} = 1 - {\varepsilon _k})$$ and 1.0.

_RP(6)_ = $${a_{fm}}$$ Constant fracture-matrix interaction reduction factor, in combination with Active Fracture Model (see online user manual)

_RP(7)_ = _ζ_ (default = 1/3)

