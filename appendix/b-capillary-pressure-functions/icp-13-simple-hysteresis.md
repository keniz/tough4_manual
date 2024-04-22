# ICP=13  Simple hysteresis

_ICP_ = 13       Simple hysteresis

An approximate hysteretic formulation based on the simple hysteresis theory of Patterson and Falta (2012) has been implemented. The simple hysteresis model is invoked by setting both _IRP_ and _ICP_ to 13. Currently, this option is only available when ECO2N is being used.

&#x20;

The capillary pressure is the van Genuchten (1980) function

$${P_c} =  - {P_0}{({\bar S_{wn}}^{ - 1/m} - 1)^{1 - m}}$$&#x20;

where

$${\bar S_{wn}} = \frac{{{S_w} - {S_{wr}}}}{{1 - {S_{wr}} - {S_{nr}}}}$$

and $$S_{wr}$$ and $$S_{nr}$$ are the residual saturations of the wetting phase and the non-wetting phase, respectively, and $$S_{nr}$$  is a variable calculated as described in  Appendix A for _IRP_ = 13.  If is greater than or equal to one, then the capillary pressure is set to zero.  For $$S_{w}$$  <  $$S_{wr}$$+ $$\varepsilon$$, _Pc_ is a linear extension that smoothly connects to the van Genuchten (1980) function and is capped by $$P_{c,max}$$ .

Parameters:

&#x20;                           _CP(1)        m_

&#x20;                           _CP(2)_ $$S_{wr}$$

&#x20;                           _CP(3)        1/_ $$P_0$$ \[Pa-1]

&#x20;                           _CP(4)_        If _>_ 1 _=_ $$P_{c,max}$$ \[Pa] (e = 1E-5)

&#x20;                                               If < 1 = e ( $$P_{c,max}$$ = 1E50 Pa)

&#x20;                                               If = 0, e = 1E-5,  $$P_{c,max}$$=1E50 Pa

&#x20;                           _CP(5)_         $$S_{ls}$$ (recommend 1)

&#x20;                           _CP(6)_        0 unless Active Fracture Model is invoked (untested)

&#x20;                           _CP(7)_        If <0 =  $$-f_{snr}$$ in linear trapping model

&#x20;                                               If >0 =  $$S_{nr ,max}$$ in Land trapping model
