# Mass-Balance Equation

The mass and energy balance are based on the general idea of conservation of mass and energy in any space. The amount of mass/energy remains constant--it is neither created nor destroyed during any chemical, physical or/and biological processes. The basic mass- and energy balance equations solved by TOUGH codes can be written in the general form:

$$\frac {d}{dt} \displaystyle  \int _{V_n}M^kdV_n=\int_{\Gamma_n}F_ k\centerdot \bold{n}d\Gamma_n+\int _{V_n}q^kdV_n$$                                                  (4-1)

The integration is over an arbitrary subdomain $$V_n$$ of the flow system under study, which is bounded by the closed surface $$\Gamma_n$$. The quantity _M_ appearing in the accumulation term (left-hand side) represents the mass of component _k_ (e.g., water, brine, gases, tracers, radionuclides, VOCs) or energy (_k_ = _h_) per volume. _**F**_ denotes mass or heat flux, and _q_ denotes sinks and sources. _**n**_ is a normal vector on the surface element $$d\Gamma_n$$, pointing inward into$$V_n$$ . Each term constituting the equations is described in detail in the following subsections.
