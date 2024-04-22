# ICP=7  van Genuchten function

van Genuchten function (van Genuchten, 1980)                                                                                              &#x20;

$$P_{cap}\quad=\quad-P_0(\;[S^*]^{1/λ}-1)^{1-λ}$$&#x20;

&#x20;subject to the restriction &#x20;

&#x20;$$-P_{max}\leqslant P_{cap}\leqslant 0$$

Here,&#x20;

$$S^*=(S_l-S_{lr})/(S_{ls}-S_{lr})$$

Parameters:     &#x20;

_CP(1)_ = $$\lambda$$ = 1 - 1/_n_

_CP(2)_ = $$S_{lr}$$     (should be chosen smaller than the corresponding  parameter in the relative permeability function; see note below.)

_CP(3)_ = 1/ $$P_0$$ = $$\alpha/\rho_wg$$ (proportional to $$\sqrt{k}$$)

_CP(4)_ = $$P_{max}$$

_CP(5)_ = $$S_{ls}$$

Notation: Parameter $$\lambda$$ is _m_ in van Genuchten’s notation, with _m_ = 1 - 1/_n_;                                      parameter _n_ is often written as $$\beta$$.

Note on parameter choices: In van Genuchten’s derivation (1980), the parameter $$S_{lr}$$for irreducible water saturation is the same in the relative permeability and capillary pressure functions. As a consequence, for $$S_l\ne S_{lr}$$we have $$k_{rl} \ne 0$$and $$P_{cap}\ne$$-∞, which is unphysical because it implies that the radii of capillary menisci go to zero as liquid phase is becoming immobile (discontinuous). In reality, no special capillary pressure effects are expected when liquid phase becomes discontinuous. Accordingly, we recommend to always choose a smaller $$S_{lr}$$for the capillary pressure as compared to the relative permeability function.
