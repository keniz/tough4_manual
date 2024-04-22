# IRP=13  Simple hysteresis

The regular hysteresis option (_IRP_ = _ICP_ = 12) provides a rigorous representation of hysteretic relative permeability and capillary pressure curves.  However, it can significantly slow down TOUGH simulations, because small time steps are often required at turning points, when a grid block switches between drainage and imbibition, because the slopes of the characteristic curves are discontinuous. Moreover, several control parameters are needed, which generally must be determined by trial and error, for the code to run smoothly.  An alternative means of capturing the essence of hysteresis, while maintaining continuous slopes and requiring no additional control parameters, is the simple hysteresis algorithm of Patterson and Falta (2012), which is invoked with _IRP_ = _ICP_ = 13

The Mualem (1976) relative permeability model is used for the non-wetting phase:

$${k_{rn}} = \sqrt {1 - {{\bar S}_{wn}}} {(1 - {\bar S_{wn}}^{1/m})^{2m}}\$$

where

$${\bar S_{wn}} = \frac{{{S_w} - {S_{wr}}}}{{1 - {S_{wr}} - {S_{nr}}}}$$

and  $$S_{wr}$$  and  $$S_{nr}$$  are residual saturations of the wetting and non-wetting phases, respectively.  Hysteresis is implemented by considering  $$S_{nr}$$  to be a variable, which is calculated from the maximum historical non-wetting phase saturation in a grid block,  $$S_{nmax}$$ .  The user has the option to specify _Snr_ as a linear function of the historical $$S_{nmax}$$ :

$${S_{nr}} = {f_{snr}}{S_{n\max }}$$

or  $$S_{nr}$$  can be calculated using a modified form of the Land (1968) relationship

$${S_{nr}} = \frac{{{S_{n\max }}}}{{1 + C{S_{n\max }}}}$$

with&#x20;

$$C = \frac{1}{{{S_{nr\max }}}} - \frac{1}{{1 - {S_{wr}}}}$$

where $$f_{snr}$$  and $$S_{nmax}$$ , the maximum residual non-wetting phase saturation, are user-specified material properties.  $$S_{nr}$$  is calculated during every Newton-Raphson iteration. If  $$S_{n}$$  drops below   $$S_{nr}$$   by dissolution or compression,  $$S_{nmax}$$ is recalculated as

$${S_{n\max }} = \frac{{{S_n}}}{{{f_{snr}}}}$$ or $${S_{n\max }} = \frac{{{S_n}}}{{1 - C{S_n}}}$$

Wetting-phase relative permeability (non-hysteretic) is from van Genuchten (1980)

$${k_{rw}} = \sqrt {{{\bar S}_w}} {\left[ {1 - {{(1 - {{\bar S}_w}^{1/m})}^m}} \right]^2}$$

where

$${\bar S_w} = \frac{{{S_w} - {S_{wr}}}}{{{S_{ws}} - {S_{wr}}}}$$

Parameters:    &#x20;

_RP(1)_ = _m_ to use in $$k_{rw}$$

&#x20;_RP(2)_ =   $$S_{wr}$$&#x20;

&#x20;_RP(3)_ =   $$S_{ws}$$  (recommend 1)

&#x20;_RP(4)_ If <0 = - $$f_{snr}$$ in linear trapping model

&#x20;            If >0 =   $$S_{nr max}$$   in Land trapping model

_RP(5) =_ $$m_{gas}$$_, m_ to use in  $$k_{rn}$$; if zero or blank, use _RP(1)_

_RP(6)_ = power to use in first term in   $$k_{rn}$$ (default ½)

_RP(7)_ If = 0 Use ( ) in first term in   $$k_{rn}$$ (Mualem, 1976)

&#x20;          If > 0 Use $$S_g$$ in first term in   $$k_{rn}$$ (Charbeneau, 2007), so that   $$k_{rn}$$ does not go to 1 when immobile liquid phase is present

&#x20;
