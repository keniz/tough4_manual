# ICP=10  Modified Brooks-Corey Model&#x20;

A modified version of the Brooks-Corey model (Brooks and Corey, 1964) has been implemented. In order to prevent the capillary pressure from decreasing towards negative infinity as the effective saturation approaches zero, a linear function is used for saturations $$S_l$$ below a certain value $$S_{lrc}+\varepsilon$$, where $$\varepsilon$$ is a small number. The slope of the linear extrapolation is identical with the slope of the capillary pressure curve at $$S_l=S_{lrc}+\varepsilon$$. Alternatively, the capillary pressure is prevented from becoming more negative than $$-p_{c,max}$$. The modified Brooks-Corey model is invoked by setting both _IRP_ and _ICP_ to 10.

$$p_c=\left\{\begin{matrix}-p_e\left(S_{ec}\right)^{-1/\lambda}\mathrm{\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ for\ }\ S_l>(S_{lrc}+\varepsilon)\\-p_e\left(\frac{\varepsilon}{1-S_{lrc}}\right)^{-1/\lambda}+\frac{p_e}{\lambda}\frac{1}{1-S_{lrc}}\left(\frac{\varepsilon}{1-S_{lrc}}\right)^{-\frac{1+\lambda}{\lambda}}\left(S_l-S_{lrc}-\varepsilon\right)\mathrm{\ \ \ \ for\ }\ S_l<(S_{lrc}+\varepsilon)\\\end{matrix}\right.$$

$$p_c\geq-p_{c,max}$$

where

$$S_{ec}=\frac{S_l-S_{lrc}}{1-S_{lrc}}$$

Parameters:     &#x20;

_CP(1)_: _λ_ (pore size distribution index)&#x20;

_CP(2)_: _Pe_ (gas entry pressure \[Pa])

&#x20;      if _CP(2)_ is negative and _USERX(1,N)_ is non-zero, apply Leverett’s rule: &#x20;

&#x20;             $$P_e=-\mathrm{\mathrm{CP}}(2)\sqrt{\mathrm{USERX}(\mathrm{1,N})\mathrm{/PER}(\mathrm{NMAT})}$$

&#x20;      if _USERX(2,N)_ is positive, _Pe_ = _USERX(2,N)_

&#x20;      if _USERX(2,N)_ is negative, _Pe_ = -_USERX(2,N)_∙_CP(2)_

_CP(3)_: _ε_ or _Pc,max_

&#x20;      if _CP(3)_ = 0, $${p}_{c,max}=10^{50}$$, $$\varepsilon=-1$$

&#x20;      if 0 < _CP(3)_ < 1, use linear model for $$S_l<S_{lrc}+\varepsilon$$

&#x20;      if _CP(3)_ $$\geq 1$$  , $$p_{c,max}$$= _CP(3)_, $$\varepsilon=-1$$

&#x20; _CP(6)_: $$S_{lrc}$$
