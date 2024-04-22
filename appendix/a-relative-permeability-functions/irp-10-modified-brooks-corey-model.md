# IRP=10  Modified Brooks-Corey Model&#x20;

_IRP_ = 10         Modified Brooks-Corey Model

A modified version of the Brooks-Corey model (Luckner et al., 1989) has been implemented to prevent the capillary pressure from decreasing towards negative infinity as the effective saturation approaches zero. The modified Brooks-Corey model is invoked by setting both _IRP_ and _ICP_ to 10.

$${{k}_{rl}}={{S}_{ek}}^{\frac{2+3\lambda }{\lambda }}$$

$${{k}_{rg}}=\left\{ \begin{matrix}    {{\left( 1-{{S}_{ek}} \right)}^{2}}\left( 1-{{S}_{ek}}^{\frac{2+\lambda }{\lambda }} \right)\text{    if RP(3) }=\text{ 0}  \\    1-{{k}_{rl}}\text{                            if RP(3) }\ne \text{ 0}  \\ \end{matrix} \right.$$

where

$${S_{ek}} = \frac{{{S_l} - {S_{lrk}}}}{{1 - {S_{lrk}} - {S_{gr}}}}$$



Parameters: _RP(1)_ = $${S_{lrk}}$$

_RP(2)_ =  $${S_{gr}}$$

_RP(3)_ = flag to indicate which equation is used for $$k_{rg}$$

