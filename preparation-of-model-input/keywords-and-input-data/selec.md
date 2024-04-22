# SELEC

**SELEC**TION      (optional) introduces a number of integer and floating-point parameters that are used for different purposes in different EOS modules or some not so often used program options. The use of this record for different EOS modules can be found in the [discussion of the modules](../../process-modeling/). The additional program options can be found in [Appendix C](../../appendix/c-additional-program-options.md).

Record **SELEC.1**

Free format for 16 or less parameters, or Format (16I5)

&#x20;                        IE(I), I=1,16

&#x20;_IE(1)_                number of records with floating point numbers that will be read (default is _IE(1)_ = 1; maximum values is 64).

Record **SELEC.2**, **SELEC.3**, ..., **SELEC.IE(1)\*8**

&#x20;                       Free format for 8 or less parameters, or Format (8E10.4)

&#x20;                       FE(I), I=1, IE(1)\*8

provide as many records with floating point numbers as specified in _IE(1)_, up to a maximum of 64 records.

An alternative input for IE and FE is directly presented as (one for each line):

&#x20;                       IE(n) = (an integer)

&#x20;                       FE(n) = (a real data)

The alternative input must appear after the normal input for IE and FE, if normal inputs exist. You can input as many as you need in this way.

**Used in**: All EOS modules

**Example**:

_SELEC_

_1, 0\*14, 1_

_0.0, 0.8, 0.8_

_ie(17) = -1              // both lower or upper case for iE and Fe input are allowed._&#x20;

_IE(30) = 50_

_FE(100)=0.5_
