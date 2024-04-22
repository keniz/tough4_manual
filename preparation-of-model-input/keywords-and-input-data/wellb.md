# WELLB

**WELLB**         provides data for wellbore simulation using drift model.

Record **WELLB.1**

&#x20;                       Free format for 7 parameters

&#x20;                        solidFrac, MaxC0, ku, WellFrac, Epson, sg1, bhExchange  (Apply to all well sections)

_SolidFrac_         Solid fraction (only used if one wants to increase thermal stability of wellbore cells by including a skin of rock around wellbore or a core of solid inside an annular tunnel in calculation of energy balance but not invoke the usage of the x material). This solid fraction would not affect anything else (e.g., the volume of wellbore cell in fluid flow calculation).

_MaxC0_           the maximum value of the profile parameter (Cmax).

_ku_                    critical Kutateladze number.

_WellFrac_         well fraction.

_Epson_             roughness parameter of the well wall.

_Sg1_                  parameter.

_btExch_           borehole heat exchange with surrounding rocks, TRUE or FALSE.

Record **WELLB.2.1** （optional)

&#x20;                        Free format for multiple parameters

&#x20;                        ActionWord, para\_1, ......, para\_n

_ActionWord   a_ string which can be a rock name, "GEOTH", or "REGFX"

If _ActionWord_ is a rock name, parameters for specific well section defined by this rock will be inputted. The parameters are:&#x20;

&#x20;                        RockName_,_ roughness, perforationF, CSArea, surFMulti, outdiam, perimeter   &#x20;

_RockName    t_he rock name for a well section to which the following 6 parameters will be applied to. The rock must be defined in the keyword "[ROCKS](rocks.md)" for a well section.&#x20;

_roughness_       roughness parameter of the well wall at this well section.

_perforationF_   perforation (screen) fraction at this well section.

_CSArea_             cross-section area at this well section.

&#x20;_surFMulti_         multipler for side surface area describing nozal effect for "x" type well at this section.

_outdiam_            wellbore outside diameter at this section

_perimeter_          perimeter of the pipe at this well section

If  _ActionWord_ is "GEOTH", parameters for calculation of the initial temperatures in the model domain will be inputted.   The parameters are:&#x20;

&#x20;                          GEOTH, GrToAll, ref\_temp, ref\_elev1, T\_grad1 , ref\_elev2, T\_grad2, ......&#x20;

_GrToAll_              indicator for geothermal gradients applying range, =0 apply to well elements only, >0 apply to all model elements.

_ref\_temp_          reference temperature at the elevation ref\_elev1.

_ref\_elev1_           the lowest reference elevation level.

_T\_grad1_             temperature gradient at the elevation ref\_elev1

_ref\_elev2_           the second reference elevation level.

_T\_grad2_             temperature gradient at the elevation ref\_elev2

As many as 4 reference elevations and temperature gradients can be inputted.

If  _ActionWord_ is "REGFX", parameters for assigning known mass flow rate to a well face will be inputted.  The parameters are:&#x20;

&#x20;                          REGFX, FaceName, iniTarget, TransTime, maxTarget, Nsteps

_FaceName_       the name of a well face that the mass flow rate will apply to. It must be identical to the connection name of two elements in the wellbore.&#x20;

_iniTarget_          the mass flow rate at time 0, a negative value indecates flow from Cell 1 to Cell 2 (kg/s).

_TransTime_      end time of flow rate transition period (s).

_maxTarget_      total mass flow rate at the end of transition period (kg/s).

_Nsteps_               number of tabular flow rate

If Nsteps>0, additonal Nsteps data records are required.

Record **WELLB.2.2** （required only when Nsteps>0)

&#x20;                           rcTime, flowRate

_rcTime_                time for mass flow rate change (s).

_flowRate_            flow rate at the time rcTime (kg/s).

Repeat data record WELLB.2.2 Nsteps times.

**Used in**: All EOS modules

**Example**

_WELLB_&#x20;

_0.0, 1.2, 1.53, 1.0, 0.046e-3,  , true                //solidfac, maxc0, ku, wellfraction, Epson, , btExch_&#x20;
