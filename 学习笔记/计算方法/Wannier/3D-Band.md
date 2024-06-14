```
!> bulk band structure calculation flag
&CONTROL
BulkBand_plane_calc = T
/

&SYSTEM
NumOccupied = 1         ! 计算NumOccupied附近的4条鞥带
SOC = 0                 ! soc
E_FERMI =  -1.2533      ! e-fermi
/

&PARAMETERS
Nk1 = 201          ! number k points
Nk2 = 201          ! number k points
/

KPLANE_BULK   ! fractional coordinates
   0.333333  0.333333  0.000000   ! 3D能带图的原点位置
   0.100000  0.000000  0.000000   ! 第一个向量的方向与大小
   0.000000  0.100000  0.000000   ! 第二个向量的方向与大小
```
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404231108318.png)

- 第7- 10列是每个k点的能量。这里我们只打印出费米能级周围的4个能带。它取决于NumOccupied。通常，我选择第4列和第5列作为k坐标，选择8和9作为能带。
