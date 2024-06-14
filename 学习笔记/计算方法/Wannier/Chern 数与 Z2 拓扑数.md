# Chern 数
**适用体系**：时间反演对称打破（有磁性）
```
&CONTROL
Chern_3D_calc = T
/

&PARAMETERS
NumOccpuied = 18  ! No. of occupied wannier bands
Nk1 = 41    ! No. of slices of the k points for WCCs
Nk2 = 41    ! No. of slices of the k points for WCCs
/

KPLANE_BULK
0.00  0.00  0.00   ! Original point for 3D k slice  k3=0
1.00  0.00  0.00  
0.00  1.00  0.00   
```

# Z2 拓扑数
**适用体系**：时间反演对称保护（非磁，`MAGMOM=100*0`）
```
&CONTROL
Z2_3D_calc = T
/

&PARAMETERS
NumOccpuied = 18  ! No. of occupied wannier bands
Nk1 = 41    ! No. of slices of the k points for WCCs
Nk2 = 41    ! No. of slices of the k points for WCCs
/

KPLANE_BULK
0.00  0.00  0.00   ! Original point for 3D k slice  k3=0
1.00  0.00  0.00  
0.00  0.50  0.00   
```
- About the Z2 index for 3D system.
$$v0= (z2(ki=0)+z2(ki=0.5))mod 2$$
$$vi= z2(ki=0.5)$$
# 通用WannierCenter
```
&CONTROL
 WannierCenter_calc=T
/

&SYSTEM
NumOccupied = 10        ! Number of occupied Wannier orbitals
/

&PARAMETERS
Nk1 = 41    ! No. of slices for the 1st reciprocal vector
Nk2 = 41    ! No. of slices for the 2st reciprocal vector
/

KPLANE_BULK
0.00  0.00  0.00   ! Original point for 3D k slice  k3=0
1.00  0.00  0.00   ! 
0.00  0.50  0.00   ! Z2设0.5， Chern数设1
```
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404291002076.png)
