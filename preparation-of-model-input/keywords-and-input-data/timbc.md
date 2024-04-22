# TIMBC

**TIMBC**            permits the users to specify time-dependent Dirichlet boundary conditions. All values in this data block are read in free format.

Record **TIMBC.1**

&#x20;                       NTPTAB

_NTPTAB_          number of elements with time-dependent boundary conditions.

Record **TIMBC.2**    (be careful, this record does not compatible with TOUGH3 input)

&#x20;                       BEleName, NBCP, NBCPV&#x20;

_BEleBame_        name of boundary element

_NBCP_               number of times.

_NBCPV_            numbering of primary variable that is time dependent, e.g., 1 for pressure. It can be different for different EOS module and different phase state condition.&#x20;

Record **TIMBC.3**

&#x20;                       TIMBCV, PGBCEL

_TIMBCV_          time of primary variable _NBCPV_ at boundary element _BCELM_

_PGBCEL_          value of primary variable _NBCPV_ at boundary element _BCELM_ at time _TIMBCV_

&#x20;                       Repeat TIMBC.3 for _NBCP_ times.

&#x20;                       Repeat records TIMBC.2, TIMBC.3 for all _NPTTAB_ elements.

**Used in**: All EOS modules

**Example**

_TIMBC_

_2                                            // time-dependent first-type boundary at 2 elements_&#x20;

_ELEM1, 3, 1                         // 1st element name, change at 3 times, time-dependent: 1st PV_&#x20;

_1000.0, 1.0e7                     //time1, the value of 1st primary variable at time1_

_2000.0, 2.0e7                    //time2, the value of 1st primary variable at time2_

_4000.0, 2.5e7                    //time3, the value of 1st primary variable at time3_

_ELEM2, 2, 4                       // 1st element name, change at 2 times, time-dependent: 4th PV_&#x20;

_2000.0, 40.0                     // time1, the value of 4th primary variable at time1_

_4000.0, 45.0                     // time2, the value of 4th primary variable at time2_
