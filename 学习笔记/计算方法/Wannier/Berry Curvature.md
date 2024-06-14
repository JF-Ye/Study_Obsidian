```
&CONTROL
BerryCurvature_calc=T
/

&SYSTEM
NumOccupied = 8         ! Number of occupied Wannier orbitals
/

&PARAMETERS
Nk1 = 101    ! No. of slices for the 1st reciprocal vector
Nk2 = 101    ! No. of slices for the 2st reciprocal vector
/

KPLANE_BULK
0.00  0.00  0.00   ! Central point for 3D k slice  k3=0
1.00  0.00  0.00   ! 第一个向量，沿此方向积分得到WCC
0.00  1.00  0.00   ! 第二个向量
```
贝利曲率是对 NumOccupied **占据带** 的求和

## 作图
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404241439114.png)
贝利曲率是对 NumOccupied **占据带** 的求和，故用 `Sum over 1-NumOccupied bands` 作图
### 步骤
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404241442465.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404241455318.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404241456064.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404241456374.png)
