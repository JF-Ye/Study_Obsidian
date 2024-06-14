# 一、计算步骤
参考文献：[Phys. Rev. B(2021) - Tunable anomalous Hall transport in bulk and two-dimensional $1T-{\mathrm{CrTe}}_{2}$: A first-principles study ](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.103.045114)

Zotero 链接：[点击这里](zotero://open-pdf/library/items/AI4Z7GHF?page=1)

地址：[Wannier90 霍尔电导率的计算(AHC) - Hexo (bowenphys.github.io)](https://bowenphys.github.io/2022/04/27/Wannier90%20%E9%9C%8D%E5%B0%94%E7%94%B5%E5%AF%BC%E7%8E%87%E7%9A%84%E8%AE%A1%E7%AE%97(AHC)/)
## 1. 准备文件
wannier90.chk；wannier90.eig；wannier90.mmn
**wannier90.spn（自旋霍尔需要）**
### 生成wannier90 .spn 步骤：
- 将 wannier 90 的非自洽步骤产生的 WAVCAR 弄到 windows 本地（自洽的 WAVCAR 不行，此时 wannier 90 产生的 WAVCAR 的 K 点数量为 KPOINTS 乘积）
- 在本地文件夹终端运行 `python -m wannierberri.utils.vaspspn` 生成 wannier. Spn 文件

## 2. postw90.x 参数
```
# 计算霍尔电导
berry = ture 			#打开berry计算开关
berry_task = ahc  		#反常：ahc；自旋：shc
fermi_energy_min = -4  		#能量范围，
fermi_energy_max = 1  		#取值基于费米能级加减x
berry_kmesh = 400 400 1		#计算网格
berry_curv_adpt_kmesh = 5	#贝里曲率值超过100 Bohr^2的k点附近，采用5x5x5的自适应加密来增加收敛性
berry_curv_adpt_kmesh_thresh = 100.0 #
fermi_energy_step = 0.1		#用于设置能量扫描步长
```
```
# 能带分辨霍尔电导
kpath = true
kpath_task = bands+shc
kpath_bands_colour = shc
kpath_num_points = 400
kubo_adpt_smr = false
kubo_smr_fixed_en_width = 1	# 调节结果的可视化
fermi_energy = 0.243
berry_curv_unit = ang2

begin kpoint_path
K 0.3333 0.3333 0.0 G 0.0 0.0 0.0
G 0.0 0.0 0.0 M 0.5 0.0 0.0
M 0.5 0.0 0.0 K 0.3333 0.3333 0.0
end kpoint_path
```
```
fermi_energy = -2.09 		#在scf的OUTCAR  
berry_curv_unit = bohr2 	#选择单位  
kslice = true 			# 是否切面  
kslice_task = curv+fermi_lines 	#计算曲率和费米线  
kslice_corner = -0.5 -0.5 0.0 	# 切面中心 
kslice_b1 = 1.0 0 0 # 这两个是面参数，两条线决定一个面  
kslice_b2 = 0 1.0 0 #  
kslice_2dkmesh = 400 400 # K撒点
```


# 二、作图
- 调用 `wannier 90-kslice-curv_x+fermi_lines.py` 脚本生成布里渊区反常霍尔
## 注意问题 ：
### 1 . 由于 `matplotlib.mlab.griddata` 在较新的 `matplotlib` 版本中已被弃用。可以使用 `scipy.interpolate.griddata` 来替代。
 - 解决方法：
 将 ` valint = ml.griddata(points_x, points_y, val_log, xint, yint)` 更改为 `valint = interpolate.Griddata ((points_x, points_y), val_log, (grid_x, grid_y), method='nearest')`；
### 2 . 插值问题：`band = interpolate.griddata((points_x, points_y), bbands[:, i], (grid_x, grid_y), method='nearest')`
- 理解
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405291632635.png)
### 3. 费米能级等高线
```
ef = -2.050000		# 定义费米能级
bands = np.loadtxt('wannier90-kslice-bands.dat')
numbands = bands.size // num_pt

bbands = bands.reshape((num_pt, numbands))
np.savetxt('reshaped_bands.dat', bbands) #保存bbands

bandint = []
grid_x, grid_y = np.meshgrid(xint, yint)

for i in range(numbands):
    bandint.append(interpolate.griddata((points_x, points_y), bbands[:, i], (grid_x, grid_y), method='nearest'))
    pl.contour(grid_x, grid_y, bandint[i], [ef], colors='black')
```
- 在绘制等高线图时，`bandint[i]` 提供了在网格 `grid_x, grid_y` 上，第 `i` 个能带的 z 值（能带值），使得 `pl.contour(grid_x, grid_y, bandint[i], [ef], colors='black')` 可以绘制出该能带在特定能级 `ef` 下的等高线。
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405292209486.png)
- 通过 `np.savetxt('reshaped_bands.dat', bbands)` 把能带变成 num_KPOINTS(行)\*num_bands (列) 的文件，挑选上一步能画出费米能级的能带用 origin 作等高线图
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405292211861.png)
### 4. 自旋/反常贝利曲率
```
val = np.loadtxt('wannier90-kslice-curv.dat', usecols=(0,))

val_log = np.array([np.log10(abs(elem)) * np.sign(elem) if abs(elem) > 10 else elem / 10.0 for elem in val])

np.savetxt('re_curv_x.dat',val_log)
```
- 先对 `wannier90-kslice-curv.dat` 文件中 x 轴的贝利曲率进行数据处理，将绝对值大于 10 的元素取对数（保持符号），对于绝对值小于等于 10 的元素，除以 10。
- 将处理后的数据存入 `re_curv_x.dat`，结合前面的二维坐标可以画出反常霍尔效应的贝利曲率图。
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405292320297.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405292323652.png)
![1716995209557.jpg](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405292324350.jpg)


### 5.修改后代码 ：
 ```
 import pylab as pl
 import numpy as np
 from scipy import interpolate
 from collections import OrderedDict
 
 points = np.loadtxt('wannier90-kslice-coord.dat')
 # Avoid numerical noise
 points_x = np.around(points[:, 0], decimals=10)
 points_y = np.around(points[:, 1], decimals=10)
 num_pt = len(points)
 
 area = 3.316560
 
 square = False
 
 if square:
     x_coord = list(OrderedDict.fromkeys(points_x))
     y_coord = list(OrderedDict.fromkeys(points_y))
     dimx = len(x_coord)
     dimy = len(y_coord)
 else:
     xmin = np.min(points_x)
     ymin = np.min(points_y)
     xmax = np.max(points_x)
     ymax = np.max(points_y)
     a = np.max(np.array([xmax - xmin, ymax - ymin]))
     num_int = int(round(np.sqrt(num_pt * a**2 / area)))
     xint = np.linspace(xmin, xmin + a, num_int)
     yint = np.linspace(ymin, ymin + a, num_int)
 
 # Energy level for isocontours (typically the Fermi level)
 ef = -2.050000
 
 bands = np.loadtxt('wannier90-kslice-bands.dat')
 numbands = bands.size // num_pt
 if square:
     bbands = bands.reshape((dimy, dimx, numbands))
     for i in range(numbands):
         Z = bbands[:, :, i]
         pl.contour(x_coord, y_coord, Z, [ef], colors='black')
 else:
     bbands = bands.reshape((num_pt, numbands))
     bandint = []
     grid_x, grid_y = np.meshgrid(xint, yint)  # 添加这一行
     for i in range(numbands):
         bandint.append(interpolate.griddata((points_x, points_y), bbands[:, i], (grid_x, grid_y), method='nearest'))
         pl.contour(grid_x, grid_y, bandint[i], [ef], colors='black')
 
 outfile = 'wannier90-kslice-curv_x.pdf'
 
 val = np.loadtxt('wannier90-kslice-curv.dat', usecols=(0,))
 
 val_log = np.array([np.log10(abs(elem)) * np.sign(elem) if abs(elem) > 10 else elem / 10.0 for elem in val])
 
 if square:
     Z = val_log.reshape(dimy, dimx)
     mn = int(np.floor(Z.min()))
     mx = int(np.ceil(Z.max()))
     ticks = range(mn, mx + 1)
     pl.contourf(x_coord, y_coord, Z, ticks, origin='lower')
 else:
     valint = interpolate.griddata((points_x, points_y), val_log, (grid_x, grid_y), method='nearest')  # 修改这一行
     mn = int(np.floor(valint.min()))
     mx = int(np.ceil(valint.max()))
     ticks = range(mn, mx + 1)
     pl.contourf(xint, yint, valint, ticks)
 
 ticklabels = []
 for n in ticks:
     if n < 0:
         ticklabels.append('-$10^{%d}$' % abs(n))
     elif n == 0:
         ticklabels.append(' $%d$' % n)
     else:
         ticklabels.append(' $10^{%d}$' % n)
 
 cbar = pl.colorbar()
 cbar.set_ticks(ticks)
 cbar.set_ticklabels(ticklabels)
 
 ax = pl.gca()
 ax.xaxis.set_visible(False)
 ax.yaxis.set_visible(False)
 
 pl.savefig(outfile, bbox_inches='tight')
 pl.show()
 
 ```


# 网页截图备份
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404152201980.png)
