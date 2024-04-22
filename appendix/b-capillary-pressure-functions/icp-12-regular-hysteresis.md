# ICP=12  Regular hysteresis

_ICP_ = 12       Regular hysteresis

The hysteretic form of the van Genuchten model (Parker and Lenhard, 1987; Lenhard and Parker, 1987) has been implemented. Details of the implementation are described in Doughty (2013). The hysteretic model is invoked by setting both _IRP_ and _ICP_ to 12.

$${P_c} =  - P_0^p{\left[ {{{\left( {\frac{{{S_l} - {S_{l\min }}}}{{1 - S_{gr}^\Delta  - {S_{l\min }}}}} \right)}^{ - \left( {\frac{1}{{{m^p}}}} \right)}} - 1} \right]^{(1 - {m^p})}}$$

where

$$S_{_{gr}}^\Delta  = \frac{1}{{1/(1 - S_l^\Delta ) + 1/{S_{gr\max }} - 1/(1 - {S_{lr}})}}$$

_CP(1)_ = $$m^d$$; van Genuchten _m_ for drainage branch $$P_{c}^d(S_l)$$.

&#x20;

_CP(2)_ =  $$S_{lmin}$$; saturation at which original van Genuchten _Pc_ goes to infinity. &#x20;

Must have   $$S_{lmin}$$<   $$S_{lr}$$ , where $$S_{lr}$$  is the relative permeability parameter _RP(2)_.

&#x20;

_CP(3)_ =  $$P_{0}^d$$; capillary strength parameter for drainage branch  $$P_{c}^d(S_1)$$ \[Pa].

&#x20;

_CP(4)_ =  $$P_{c,max}$$; maximum capillary pressure \[Pa] obtained using original van Genuchten $$P_c$$. Inverting the original van Genuchten function for  $$P_{c,max}$$ determines $$S_m$$, the transition point between the original van Genuchten function and an extension that stays finite as  $$S_l$$ goes to zero. For functional form of extension, see description of _CP(13)_ below.

&#x20;

_CP(5)_ = scale factor for pressures for unit conversion (1 for pressure in Pa).

&#x20;

_CP(6)_ = $$m^w$$; van Genuchten _m_ for imbibition branch  $$P_{c}^w(S_l)$$. Default value is _CP(1)_ (recommended unless compelling reason otherwise).

&#x20;

_CP(7)_ = $$P_w^0$$; capillary strength parameter for imbibition branch   $$P_{c}^w(S_l)$$ \[Pa]. Default value is _CP(3)_ (recommended unless compelling reason otherwise).

&#x20;

_CP(8)_ = parameter indicating whether to invoke non-zero _Pc_ extension for $$S_l$$ > $$S_l^*$$&#x20;

\= 1 – $$S_{gr}^\Delta$$

&#x20;\=0        no extension; $$P_c$$ = 0 for  $$S_l$$ > $$S_l^*$$&#x20;

\>0        power-law extension for  $$S_l^*$$ <$$S_l$$  <1, with $$P_c$$ = 0 when  $$S_l$$ = 1. A non-zero _CP(8)_ is the fraction of $$S_l^*$$ at which the _Pc_ curve departs from the original van Genuchten function. Recommended range of values: 0.97–0.99.&#x20;

&#x20;

_CP(9)_ = flag indicating how to treat negative radicand, which can arise for  $$S_l$$>  $$S_l^{\Delta23}$$  for second-order scanning drainage curves (_ICURV_ = 3), where $$S_l^{\Delta23}$$  is the turning-point saturation between first-order scanning imbibition (_ICURV_ = 2) and second-order scanning drainage. None of the options below have proved to be robust under all circumstances. If difficulties arise because $$S_l$$>  $$S_l^{\Delta23}$$  for _ICURV_ = 3, also consider using _IEHYS(3)_ > 0 or _CP(10)_ < 0, which should minimize the occurrence of $$S_l$$>  $$S_l^{\Delta23}$$  for _ICURV_ = 3.

\=0        radicand = max(0,radicand) regardless of $$S_l$$ value

\=1        if $$S_l$$>  $$S_l^{\Delta23}$$ , radicand takes value of radicand at $$S_l$$=  $$S_l^{\Delta23}$$&#x20;

\=2        if $$S_l$$>  $$S_l^{\Delta23}$$ , use first-order scanning imbibition curve (_ICURV_ = 2)

&#x20;

_CP(10)_ = threshold value of $$\vert \Delta S \vert$$ (absolute value of saturation change since previous time step) for enabling a branch switch (default is 1E-6; set to any negative number to do a branch switch no matter how small $$\vert \Delta S \vert$$ is; set to a value greater than 1 to never do a branch switch). See also _IEHYS(3)_.

&#x20;

_CP(11)_ = threshold value of $$S_{gr}^\Delta$$. If value of  $$S_{gr}^\Delta$$ calculated from  $$S_{l}^\Delta$$(Equation (2)) is less than _CP(11)_, use  $$S_{gr}^\Delta$$ = 0. Recommended value 0.01–0.03; default is 0.02.

&#x20;

_CP(12)_ = flag to turn off hysteresis for $$P_c$$ (no effect on   $$k _{rl}$$ and   $$k _{rg}$$; to turn off hysteresis entirely, set  $$S_{grmax}$$ = 0 in _RP(3)_).

\=0        hysteresis is on for $$P_c$$&#x20;

\=1        hysteresis is off for $$P_c$$  (switch branches of $$P_c$$  as usual, but set $$S_{gr}$$  = 0 in  $$P_c$$ calculation. Make sure other parameters of  $$P_c^d$$ and  $$P_c^w$$ are the same: _CP(1)_ = _CP(6)_ and _CP(3)_ = _CP(7)_)

&#x20;

_CP(13)_ = parameter to determine functional form of _Pc_ extension for $$S_l$$>< $$S_{lmin}$$  (i.e., $$P_c$$  > $$P_{cmax}$$ )

\=0        exponential extension

\>0        power-law extension with zero slope at $$S_l$$ = 0 and $$P_{c}(0)$$ =_CP(13)_.  Recommended value: 2 to 5 times _CP(4)_=$$P_{cmax}$$ . Should not be less than or equal to _CP(4)_.
