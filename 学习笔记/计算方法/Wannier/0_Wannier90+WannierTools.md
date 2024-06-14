# 一、前期
## 1. 自洽：生成 *WAVECAR* 和 *CHGCAR*
## 2. 计算能带，观察投影轨道，确定费米能级附近的轨道
-  注意：
	- wannier90能带拟合不好一般是由于 ***NBANDS*** 算的不够多导致
	- ***NBANDS*** 必须同时是**核数**和**NPAR**的整数倍

# 二、Wannier90
## 1. 复制POTCAR, POSCAR, WAVECAR, CHGCAR, INCAR, KPOINTS
- **KPOINTS** : 其值为格点间的 **hopping**
- **INCAR** 设置：
```
	- LWANNIER90=.T.
	- ISTART=1
	- ICHARG=11
	- NBANDS=自洽NBANDS
	- 注释NPAR
	- ISYM=-1 (在加SOC的情况下)
```
- **wannier90.win** 设置：
```
	- num_wann=投影轨道值 × 原子数 
		注：如考虑SOC，还要再乘 2
	- num_bands = NBANDS	
	- write_hr = true
	- frozen窗口详情看吴泉生老师视频
	- dis接纠缠窗口上限可以不设，避免报错
```
<div align=center> <img src="https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404112252201.png
" width = 100%/> </div>

#### 先提交vasp_wannier计算投影，再提交wannier90.x生成wannier_hr.dat文件
## 2. 检验拟合程度
- 通过wannier90_band.dat作图（**其能量数据减去第一性能带的费米能级**）
- 对比第一性原理计算的能带图
- wannier90.wout 展宽观察
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404271101549.png)


# 三、WannierTools
### 参数说明
#### KPLANE_SLAB
```
KPLANE_SLAB
0.0 0.0		! 设置平面的原点
1.0 0.0		! 平面的第一个向量方向及大小
0.0 1.0		! 第二个向量
```
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404231602011.png)
#### KPLANE_BULK
```
KPLANE_BULK	! 设置计算选取的平面
 0.00  0.00  0.00	! 3D布里渊区的原点
 1.00  0.00  0.00	! 基于原点选取的第一个向量
 0.00  1.00  0.00	! 第二个向量
```
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404231604689.png)
#### 结果参数
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404231108318.png)
- 第 1-3 列为 cartesian 坐标（实空间）。第 4-6 列为 k 空间坐标。
### 利用create_wt_in.py生成wt.in
1. [[SHC与AHC（霍尔电导）]]
2. [[Surface_dos]]