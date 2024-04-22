# ICP=11  Modified van Genuchten Model

The van Genuchten model (Luckner et al., 1989) has been modified to prevent the capillary pressure from decreasing towards negative infinity as the effective saturation approaches zero. The approach is identical to that in _ICP_=10, except that two extensions (linear and log-linear) are available. The modified van Genuchten model is invoked by setting both _IRP_ and _ICP_ to 11.

$${p_c} =  - \frac{1}{\alpha }{\left[ {{{\left( {{S_{ec}}} \right)}^{(\gamma  - 1)/m}} - 1} \right]^{1/n}}$$ for $${S_l} \ge ({S_{lrc}} + \varepsilon )$$

$${p_c} =  - \frac{1}{\alpha }{\left[ {{S_{ec*}}^{(\gamma  - 1)/m} - 1} \right]^{1/n}} - \beta  \cdot \left( {{S_l} - {S_{lrc}} - \varepsilon } \right)$$ for $${S_l} < ({S_{lrc}} + \varepsilon )$$

with

linear extension: $$\beta  =  - \frac{{(1 - \gamma )}}{{\alpha nm}} \cdot \frac{1}{{(1 - {S_{lrc}})}} \cdot {\left( {S_{ec*}^{(\gamma  - 1)/m} - 1} \right)^{\frac{1}{n} - 1}}{S_{ec*}}^{ \cdot \left( {\frac{{\gamma  - 1 - m}}{m}} \right)}$$

$${p_c} =  - \frac{1}{\alpha }{\left[ {{S_{ec*}}^{(\gamma  - 1)/m} - 1} \right]^{1/n}} \cdot {10^{\beta  \cdot \left( {{S_l} - {S_{lrc}} - \varepsilon } \right)}}$$ for $${S_l} < ({S_{lrc}} + \varepsilon )$$

with

log-linear extension:  $$\beta  =  - lo{g_{10}}(e) \cdot \left( {\frac{{1 - m}}{m} \cdot \frac{{\gamma  - 1}}{\varepsilon } \cdot \frac{1}{{S_{ec*}^{(1 - \gamma )/m} - 1}}} \right)$$

$${p_c} \ge  - {p_{c,\max }}$$

where

$${S_{ec}} = \frac{{{S_l} - {S_{lrc}}}}{{1 - {S_{lrc}}}}$$, $${S_{ec*}} = \frac{\varepsilon }{{1 - {S_{lrc}}}}$$

Parameters:    &#x20;

_CP(1)_: _n_ (parameter related to pore size distribution index,see also _CP(4)_)

&#x20;

_CP(2)_:  $${1 \mathord{\left/  {\vphantom {1 \alpha }} \right.  } \alpha }$$ (parameter related to gas entry pressure \[Pa])

&#x20;           _USERX(4,N)_>0: $$1/{\alpha _i}$$= _USERX(4,N)_

&#x20;           _USERX(4,N)_<0: $$1/{\alpha _i}$$= _USERX(4,N)·CP(2)_

if _CP(2)_ is negative, apply Leverett scaling rule:

$$1/{\alpha _i} = 1/{\alpha _{ref}} \cdot \sqrt {{k_i}/{k_{ref}}}$$

where:

&#x20;$$1/\alpha _{ref}$$=_|CP(2)|_

&#x20; $$k _{ref}$$= _PER(NMAT)_

&#x20;   _USERX(1,N)_>0:  $$k _{i}$$= _USERX(1,N)_

&#x20;    _USERX(1,N)_<0:  $$k _{i}$$= _USERX(1,N)_·_PER(NMAT)_

&#x20; _CP(3)_: _ε_ or $$P_{c,max}$$

if _CP(3)_ = 0,  $$P_{c,max}$$= $$10^{50}$$, $$\varepsilon  =  - 1$$

if 0 < _CP(3)_ < 1, =_CP(3)_ and use linear extension

if _CP(3)_ => 1,  $$P_{c,max}$$=_CP(3)_, $$\varepsilon  =  - 1$$

if –1< _CP(3)_ <0, $$\varepsilon$$ =|_CP(3)_| and use log-linear extension

&#x20; _CP(4)_: _m_

if zero then _m=_1-1/_CP(1)_,  else _m_=_CP(4)_ and _n=_1/(1-_m_)

&#x20;_CP(5)_: $$T_{ref}$$

if negative, |_CP(5)_| is reference temperature to account for temperature dependence of capillary pressure due to changes in surface tension

&#x20; _CP(6)_: _γ_ parameter of Active Fracture Model (see Appendix C)

&#x20;_CP(7)_: $$S_{lrc}$$

if zero, then $${S_{lrc}} = {\rm{ RP(1) }} = {S_{lrk}}$$

