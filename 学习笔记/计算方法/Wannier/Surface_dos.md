```
SURFACE            ! 选取面内两个非线性向量
 1  0  0 
 0  1  0        

&CONTROL
SlabSS_calc = T
/

&PARAMETERS
OmegaNum = 101
OmegaMin = -1.0    ! 能量窗口
OmegaMax =  1.0
Nk1 = 101   ! 高对称路径撒点
NP = 2      ! principle layer
/

KPATH_SLAB
2        ! numker of k line for 2D case
K 0.33 0.67 G 0.0 0.0  ! k path for 2D case
G 0.0 0.0   M 0.5 0.5
```

## KCUBE_BULK 参数无用
