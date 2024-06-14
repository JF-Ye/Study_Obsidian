```
&CONTROL
AHC_calc=T     ! 反常霍尔电导
SHC_calc=T     ！自旋霍尔电导
/

&PARAMETERS
OmegaNum = 601    ! number of slices of energy
OmegaMin = -1.0   ! erergy range for AHC
OmegaMax =  1.0
Nk1 = 51   ! No. of slices for the 1st reciprocal vector
Nk2 = 51   ! No. of slices for the 2nd reciprocal vector
Nk3 = 51   ! No. of slices for the 3nd reciprocal vector
/

KCUBE_BULK
  0.00  0.00  0.00   ! Original point for 3D k plane
  1.00  0.00  0.00   ! The first vector 
  0.00  1.00  0.00   ! The second vector
  0.00  0.00  1.00   ! The third vector
```