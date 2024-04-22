# Semi-Analytical Conductive Heat Exchange

TOUGH4 provides options for modeling linear or radial conductive heat exchange with geologic formations where no fluid exchange is considered, using semi-analytical methods. This is a much more efficient alternative to the approach that simply extends the computational grid into those formations and assigns small or vanishing permeability to them. Even to achieve modest accuracy, the number of grid blocks in the heat flow domain could easily become comparable to, or even larger than, the number of grid blocks in the fluid flow domain, leading to a very inefficient calculation. The semi-analytical methods require no grid blocks outside of the fluid flow domain, and permit better accuracy for short- and long-term heat exchange. Note that radial _and_ linear semi-analytical heat exchange cannot be combined in the current version of TOUGH4.

_**Linear Heat Exchange between a Reservoir and Confining Beds**_

TOUGH4 uses the method of Vinsome and Westerveld (1980), which gives excellent accuracy for heat exchange between reservoir fluids and confining beds such as may arise in geothermal injection and production operations. This method is developed for calculating heat losses from the reservoir to caprock or base rock and predicting the temperature profile in a semi-infinite, homogeneous, conductive half-space confining bed. Observing that the process of heat conduction tends to dampen out temperature variations, Vinsome and Westerveld suggested that caprock or base rock temperatures would vary smoothly even for strong and rapid temperature changes at the boundary of the conduction zone. Arguing that heat conduction perpendicular to the conductive boundary is more important than parallel to it, they proposed to represent the temperature profile in a semi-infinite conductive layer by means of a simple trial function, as follows:

$$T(x,t)-T_i=(T_f-T_i+px+qx^2 )  exp⁡(-x/d)$$                                                   (4-31)

where, _x_ is the distance from the boundary, $$T_i$$ is initial temperature in the cap- or base-rock (assumed uniform), $$T_f$$is the time-varying temperature at the cap- or base-rock boundary, _p_ and _q_ are time-varying fit parameters, and _d_ is the penetration depth for heat conduction, given by\
$$d=\sqrt{Θt}∕2$$                                                                                                                    (4-32)

where $$Θ=\lambda/\rho C$$ is the thermal diffusivity, $$\lambda$$the thermal conductivity, $$\rho$$ the density of the medium, and _C_ the specific heat. In the context of a finite-difference simulation of nonisothermal flow, each grid block in the top and bottom layers of the computational grid will have an associated temperature profile in the adjacent impermeable rock as given by Eq. (4-31). The coefficients _p_ and _q_ will be different for each grid block; they are determined concurrently with the flow simulation from the physical constraints of (1) continuity of heat flux across the boundary, and (2) energy conservation for the reservoir/confining layer system.

_**Radial Heat Exchange between Fluids in a Wellbore and the Surrounding Formation**_

Radial, conductive heat exchange between fluids in a discretized wellbore and the formation is calculated using a semi-analytical, time-convolution method. Note that the time-dependent temperature evolution in the fully-discretized wellbore is calculated numerically. At each time step, radial heat transfer with the formation is calculated by superposition of analytical solutions of heat flow that are dependent on the temperature differences between subsequent time steps.

Carslaw and Jaeger (1959) provided an approximate solution for heat conduction between a cylinder and surrounding media where the temperature of the cylinder is maintained constant. If the initial temperature difference between the two domains is ∆_T_ = _Tw - Tf_ (where _Tw_ and _Tf_ are the temperatures in the well and the formation, respectively), the heat flux _q_ from the wellbore to the formation can be calculated as the product of a heat transfer function and the temperature using Eq. (4-33) for small values of the dimensionless time $$t_d=\alpha t/r_0^2$$ , where _α_ is the thermal diffusivity and $$r_0$$ is the wellbore radius (m), and Eq. (4-34) for large values of $$t_d$$:

$$q=f_1 (t_d)⋅ΔT=λΔT/r_0  [(πt_d )^{-0.5}+1/2-1/4(t_d/π )^{0.5}+1/8 t_d-…]$$            (4-33)

$$q=f_2 (t_d)⋅ΔT=2λΔT/r_0  [1/(ln⁡( 4t_d)-2γ)-γ/((ln⁡( 4t_d)-2γ)^2 )-…]$$         (4-34)

where, _λ_ is thermal conductivity $$(Wm^{-1}K^{-1})$$, and _γ_ is the Euler constant (0.57722). The heat transfer functions _f1_ and _f2_ express the amount of heat flux with time due a unit temperature difference. As shown in Zhang et al. (2011), the heat transfer functions _f1_ and _f2_ are approximately the same at the dimensionless time $$t_d=2.8$$. Therefore, $$t_d=2.8$$ is considered the critical dimensionless time to switch from _f1_ to _f2_.

During fluid injection and production, and as a result of the heat exchange processes, temperature changes continuously over time at any point within the wellbore and at the wellbore-formation interface. Based on superposition, the radial heat flux across each wellbore element to the surrounding formation is a time-convolution result of varying temperature. The discretized form at each time step can be expressed as

&#x20;$$q_{total}=\displaystyle\sum_{i=1}^{d-1}f(t_d-t_i) \Delta  T(t_i)$$                                                                                             (4-35)

where, $$t_d$$ represents the current time after _d_ time steps, and $$t_i$$ represents the time after _i_ time steps; the function _f_ is _f1_ if $$t_d-t_i \le2.8$$ , and _f2_ if $$t_d=t_i>2.8$$ . The temperature difference $$\Delta T(t_i)$$ is the temperature in the well at time step _i_, minus the formation temperature at the interface at the previous time step, i.e., $$\Delta T(t_i)=T_w(t_i)-T_f(t_i-1)$$.
