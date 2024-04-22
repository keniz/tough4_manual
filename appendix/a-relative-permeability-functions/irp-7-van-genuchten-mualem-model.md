# IRP=7  van Genuchten-Mualem Model

_IRP_ = 7         van Genuchten-Mualem Model (Mualem, 1976; van Genuchten, 1980)

$$k_{rl}=\sqrt{{{S}^{*}}}\ {{\left\{ 1\ -\ {{\left( 1\ -\ {{[{{S}^{*}}]}^{{1}/{\lambda }\;}} \right)}^{\lambda }} \right\}}^{2}}\quad \text{    if}\ \text{ }{{S}_{l}}\ <\ {{S}_{ls}}$$

$$k_{rl}=1\quad \quad \quad \quad \quad \quad \quad \quad \quad \text{     }\quad \text{if}\ \text{ }{{S}_{l}}\ \ge \ {{S}_{ls}}$$



Gas relative permeability can be chosen as one of the following two forms, the second of which is due to Corey (1954)

$${{k}_{rg}}=1\ -\ {{k}_{rl}}\quad \ \quad \quad \quad \text{    if}\ {{S}_{gr}}\,=\,0$$

$${{k}_{rg}}={{\left( 1\ -\ \hat{S} \right)}^{2}}\ \left( 1\ -\ {{{\hat{S}}}^{2}} \right)\quad \text{     if}\ {{S}_{gr}}\,>\,0$$

subject to the restriction $$0\quad \le \quad {{k}_{rl}},\ {{k}_{rg}}\quad \le \quad 1$$

Here $${{S}^{*}}\quad =\quad {\left( {{S}_{l}}\ -\ {{S}_{lr}} \right)}/{\left( {{S}_{ls}}\ -\ {{S}_{lr}} \right)}\;$$and $$\hat{S}\quad =\quad {\left( {{S}_{l}}\ -\ {{S}_{lr}} \right)}/{\left( 1\ -\ {{S}_{lr}}\ -\ {{S}_{gr}} \right)}\;$$



Parameters:     _RP(1)_ = $$\lambda$$

&#x20;           _RP(2)_ = Slr

&#x20;           _RP(3)_ = Sls

&#x20;           _RP(4)_ = Sgr

&#x20;

Notation: Parameter $$\lambda$$ is m in van Genuchten’s notation, with m = 1 - 1/n;                                          parameter _n_ is often written as $$\beta$$.









