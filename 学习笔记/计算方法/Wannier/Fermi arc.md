```
SURFACE            ! 选取面内两个非线性向量
 1  0  0 
 0  1  0        

&CONTROL
SlabArc_calc=T
/

&PARAMETERS
E_arc = 0.0  ! 设置计算费米弧的能量值（减去费米能级）
Nk1 = 101    ! No. of slices for the 1st reciprocal vector
Nk2 = 101  
/

KPLANE_SLAB
0.0 0.0		! 设置平面的原点，一般 0 0 就好
1.0 0.0		! 平面的第一个向量方向及大小
0.0 1.0		! 第二个向量
```

## 注意：
- KPLANE_BULK 无用