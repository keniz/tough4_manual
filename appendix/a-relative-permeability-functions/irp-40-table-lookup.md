# IRP=40  Table lookup

The calculation for relative permeabilities is by table lookup and interpolation. The table input is through input Record[ ROCKS.1.4](../../preparation-of-model-input/keywords-and-input-data/rocks.md).

If the user wishes to employ other relative permeability relationships, these need to be programmed into subroutine RELP in module HydraulicAndThermal\_Properties（media\_Properties.f90）. The routine has the following structure:

```
 SUBROUTINE RELP(SATU,RELPERM,NMAT,USRX)
                ...
              RELP_FUNCTION: SELECT CASE (IRP(NMAT))
			CASE (1)
				CALL RELP_LINEAR(...)
			CASE (2)
				...
			...
			...
		    END SELECT RELP_FUNCTION

            END


```

To code an additional relative permeability function, the user needs to insert a code segment analogous to that shown above, beginning with a CASE option which would be identical to _IRP_ and calls a subroutine for the additional relative permeability function.
