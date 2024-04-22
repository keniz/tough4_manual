# TRACR

**TRACR**                introduces tracer parameters. &#x20;

Record **TRACR.1**

&#x20;                           Free format for 3 integer parameters.

&#x20;                           NumTracer, TracerInPhase, useRockDistrC

_NumTracer_          Number of tracers to be simulated, the maximum is 5.

_TracerInPhase_    These tracers will be in which phase: 1-Gas, 2-Aqueous, 3-Oil/Liquid (Effect for EOS1, EOS2, EOS3, EOS4, EOS6, ECO2 only).

&#x20; _useRockDistC_   How to handle the tracer distribution coefficient in different rocks,

&#x20;                            \=0, tracer distribution coefficient is the same in different rocks (input through following parameter XKD).&#x20;

&#x20;                            \>0, tracer distribution coefficient is different in different rocks (input through Record ROCKS.1.1).

In the TOUGH4, the tracers are only allowed in specified phases, except EOS7 which allows tracers in any phases, EOS9 and TMVOC in aqueous only, and EWASG in aqueous and solid phase only. The default is in aqueous phase.

Record **TRACR.2**

&#x20;                           Free format for as many as 11 parameters

TracerName, AMWTM, XHALF, XKD, InvHC, Parent1, mFrac1, Parent2, mFrac2, Parent3, mFrac3

_TracerName_       Name of the tracer

_AMWTM_              Tracer’s molecular weight, g/mole, for EOS7 and for any module involved calculation of product amount of decay/biodegradation processes only.

_XHALF_                 Half-life of this tracer, in seconds, default is 1.0e50.

_XKD_                     Distribution coefficient for this tracer in the aqueous phase, $$m^3kg^{-1}$$.

_InvHC_                 Inverse Henry's constant $$(Kh)^{-1}$$, $$Pa^{-1}$$. (The inverse Henry’s constant can be thought of as an aqueous phase solubility.), for EOS7 only.

_Parent1_             This tracer’s parent of the decay chain/biodegradation, input the tracer number of its parent, default is 0-no parent.&#x20;

_mFrac1_             Molar fraction of parent1 decay into current tracer, (default=1.0). The sum of mass fractions to all daughters from the same parent must be 1.0.

(Repeat for parent2 and parent3, the maximum 3 parents are allowed)

Repeat the record TRACR.2 for _NumTracer_ times.

**Used in**: All EOS modules

**Example**

_TRACR_

_2, 2                      //number of tracer: 2, in aqueous (1:gas, 2: aqueous)_&#x20;

_tr1, ,1.0e9, , ,      // 1st tracer name: tr1, half-life=1.0e9s, other parameters use the default values._

&#x20;_tr2, ,1.0e50, 0.001,  , 1    // 2nd: tr2, half-life=1.0e50 (no decay), XKD=0.001, its parent is tracer 1._
