# IRP=12  Regular hysteresis

_IRP_ = 12         Regular hysteresis

The hysteretic form of the van Genuchten model (Parker and Lenhard, 1987; Lenhard and Parker, 1987) has been implemented. Details of the implementation are described in Doughty (2013). The regular hysteresis model is invoked by setting both _IRP_ and _ICP_ to 12.

$${k_{rl}} = \sqrt {{{\bar S}_l}} {\left[ {1 - \left( {1 - \frac{{{{\bar S}_{gt}}}}{{1 - \bar S_l^\Delta }}} \right){{(1 - {{({{\bar S}_l} + {{\bar S}_{gt}})}^{1/m}})}^m} - \left( {\frac{{{{\bar S}_{gt}}}}{{1 - \bar S_l^\Delta }}} \right){{(1 - {{(\bar S_l^\Delta )}^{1/m}})}^m}} \right]^2}$$

$${k_{rg}} = {k_{rg\max }}{(1 - ({\bar S_l} + {\bar S_{gt}}))^\gamma }{(1 - {({\bar S_l} + {\bar S_{gt}})^{1/m}})^{2m}}$$

where

$${\bar S_l} = \frac{{{S_l} - {S_{lr}}}}{{1 - {S_{lr}}}}$$, $$\bar S_l^\Delta  = \frac{{S_l^\Delta  - {S_{lr}}}}{{1 - {S_{lr}}}}$$, $${\bar S_{gt}} = \frac{{S_{gr}^\Delta ({S_l} - S_l^\Delta )}}{{(1 - {S_{lr}})(1 - S_l^\Delta  - S_{gr}^\Delta )}}$$

$$S_{_{gr}}^\Delta  = \frac{1}{{1/(1 - S_l^\Delta ) + 1/{S_{gr\max }} - 1/(1 - {S_{lr}})}}$$

$$S_l^\Delta$$ is the turning-point saturation, and $$S_{gr}^\Delta$$ is the residual gas saturation.

_RP(1)_ = _m_; van Genuchten _m_ for liquid relative permeability (need not equal _CP(1)_ or _CP(6)_);  $$k_{rl}$$  uses the same _m_ for drainage and imbibition.

&#x20;

_RP(2)_ = $$S_{lr}$$ : $$k_{lr}(S_{lr})$$ = 0, $$k_{rg}(S_{lr}) = k_{rgmax}$$. Must have $$S_{lr}$$ > $$S_{lmin}$$ in capillary pressure (_CP(2)_).  $$S_{lr}$$  is minimum saturation for transition to imbibition branch. For  $$S_{l}$$  <  $$S_{lr}$$ , curve stays on primary drainage branch even if  $$S_{l}$$  increases.

&#x20;

_RP(3)_ = $$S_{grmax}$$; maximum possible value of  $$S_{gr}^\Delta$$ .  Note that the present version of the code requires that  $$S_{lr}$$  + $$S_{grmax}$$ < 1, otherwise there will be saturations for which neither fluid phase is mobile, which the code cannot handle. Setting  $$S_{grmax}$$  = 0 effectively turns off hysteresis. As a special option, a constant, non-zero value of _S_gr may be employed by setting _CP(10)_>1 and making _RP(3)_ negative. The code will set  $$S_{gr}^\Delta$$  = -_RP(3)_ for all grid blocks at all times.

&#x20;

_RP(4)_ = $$\gamma$$; typical values 0.33 – 0.50.&#x20;

_RP(5)_ = $$k_{rgmax}$$

_RP(6)_ = fitting parameter for _krg_ extension for  $$S_{l}$$  <  $$S_{lr}$$  (only used when  < 1); determines type of function for extension and slope of  $$k_{rg}$$ at  $$S_{l}$$ = 0.

≤ 0       use cubic spline for 0 <  $$S_{l}$$  < $$S_{lr}$$ , with slope at  $$S_{l}$$ = 0 of _RP(6)_

\> 0       use linear segment for 0 <  $$S_{l}$$  < _RP(8)Slr_ and cubic spline for _RP(8)_  $$S_{lr}$$  <  $$S_{l}$$  <  $$S_{lr}$$ _,_ with slope at  $$S_{l}$$ = 0 of –_RP(6)_.&#x20;

&#x20;

_RP(7)_ = numerical factor used for _krl_ extension to $$S_{l}$$  >  $$S_{l}^*$$ ,. _RP(7)_ is the fraction of _Sl_\* at which _krl_ curve departs from the original van Genuchten function.  Recommended range of values: 0.95–0.97. For _RP(7)_=0, _krl_ =1 for  $$S_{l}$$  >  $$S_{l}^*$$  (not recommended).

&#x20;

_RP(8)_ = numerical factor used for linear _krg_ extension to   $$S_{l}$$  <   $$S_{lr}$$  (only used when  $$k_{rgmax}$$< 1). _RP(8)_ is the fraction of  $$S_{lr}$$  at which the linear and cubic parts of the extensions are joined.

&#x20;

_RP(9)_ = flag to turn off hysteresis for  $$k_{rl}$$  (no effect on _Pc_ and  $$k_{rg}$$ ; to turn off hysteresis entirely, set  $$S_{grmax}$$  = 0 in _RP(3)_).

\=0        hysteresis is on for _krl_

\=1        hysteresis is off for _krl_ (force  $$k_{rl}$$ to stay on primary drainage branch ( $$k_rl^{d}$$) at all times)

&#x20;

_RP(10)_ =  $$m_{gas}$$ ; van Genuchten _m_ for gas relative permeability (need not equal _CP(1)_ or _CP(6)_); $$k_{rg}$$ uses same _mgas_ for drainage and imbibition. If zero or blank, use _RP(1)_ so that $$m_{gas}$$ = _m_.

&#x20;
