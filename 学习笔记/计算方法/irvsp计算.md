# [IRVSP官方文章](zotero://open-pdf/library/items/4ZDDUJQY?page=1)

## 1. 调用phonopy找到原胞
```
phonopy --symmetry --tolerance 0.01 -c POSCAR
```
## 2. 复制PPOSCAR，进入[**irvsp官网**](https://tm.iphy.ac.cn/TopMat_1651msg.html)生成POSCAR_msg，及部分INCAR参数
-  注意：
- 要在PPOSCAR第6行补上元素名称
- 根据空间群设置[**磁群**](https://www.cryst.ehu.es/cryst/magnext.php?from=mgenpos&magtr=1&radical=191&radical_label=P6/mmm)

![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404161632726.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404161632879.png)
## 3. 利用POSCAR_msg以及INCAR做自洽计算
- **注意**：
	- **注释**掉 **ISYM** 参数
	- 生成CHGCAR
## 4. 利用官网生成的 [*KPOINTS*](zotero://open-pdf/library/items/4ZDDUJQY?page=2)与 *CHGCAR* 进行**能带**计算，生成***WAVECAR***
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404161636296.png)
## 5. 调用 irvsp 生成结果
```
irvsp -sg $space_group -nb 1 $num_occupied > outir
```
###  查看电子占据带 num_occupied：确定要计算的能带序号（此处能带序号与第一性原理计算的能带序号一样
	- 方法一：
		- 看第一性原理计算的能带
	- 方法二：
		- 调用脚本irvsp_occupied观察占据带
<div align="center"> <img src="https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404112139714.png" width = 500 /> </div>

<div align="center"> <img src="https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404112143403.png" width = 500  /></div>

## 6. 进网站查看$\mathcal{Z}_2$拓扑数
- [SOC体系](https://tm.iphy.ac.cn/TopMat_1651msg.html)
- [非SOC体系](https://tm.iphy.ac.cn/UnconvMat.html)

## 7. 宇称计算 $\mathcal{Z}_2$ 拓扑数
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202406031723345.png)
![57e01013113acdda03d721efe98597c.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202406031723874.png)
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202406141019926.png)

### 公式
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202406131037749.png)
网址链接：[点这里](https://docs.quantumatk.com/tutorials/topological_insulator_bi2se3/topological_insulator_bi2se3.html#topological-invariants)

Zotero文章链接：[Topological insulators with inversion symmetry](zotero://open-pdf/library/items/6BLGPVZ9?page=2)
