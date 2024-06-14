---
tags: []
parent: 'Calculation of intrinsic spin Hall conductivity by Wannier interpolation'
collections:
    - 自旋霍尔效应
version: 203
libraryID: 1
itemKey: YFZ999P7

---
# 基于最大局域Wannier Funciton（MLWF)计算自旋霍尔电导
# [文献链接](zotero://open-pdf/library/items/MVCD5W8P)

# 一、绪论
1.  **定义**：SHE指通过施加电场可产生横向自旋电流的现象
2.  **分类**：
	1) 由能带结构直接导致的本征SHE
	2) 与散射相关的外因 side-jump SHE
	3) 与散射相关的外因 skew-scattering SHE
3. SOC起重要作用
4. 
# 二、基本理论
1. 描述**自旋霍尔电导**和**反常霍尔电导**的Kubo通用公式：
	（AHC的 $\hat{j}_{x}=-e \hat{v}_{y}$ , SHC的 $\hat{j}_{x}=\frac{1}{2}{\hat{s}_{z},\hat{v}_{x}}$
$$
\sigma_{x y}(\omega)= \frac{\hbar}{V N_{k}^{3}} \sum_{k} \sum_{n} f_{n \boldsymbol{k}}\times \sum_{m \neq n} \frac{2 \operatorname{Im}\left[\left\langle n \boldsymbol{k}\left|\hat{j}_{x}\right| m \boldsymbol{k}\right\rangle\left\langle m \boldsymbol{k}\left|-e \hat{v}_{y}\right| n \boldsymbol{k}\right\rangle\right]}{\left(\epsilon_{n \boldsymbol{k}}-\epsilon_{m k}\right)^{2}-(\hbar \omega+i \eta)^{2}}
$$
	其中，**自旋霍尔电导**的公式表示为：
$$
\sigma_{x y}^{\text {spinz }}(\omega)= \hbar \int_{\mathrm{BZ}} \frac{d^{3} k}{(2 \pi)^{3}} \sum_{n} f_{n \boldsymbol{k}}\times \sum_{m \neq n} \frac{2 \operatorname{Im}\left[\left\langle n \boldsymbol{k}\left|\hat{j}_{x}^{\mathrm{spin}}\right| m \boldsymbol{k}\right\rangle\left\langle m \boldsymbol{k}\left|-e \hat{v}_{y}\right| n \boldsymbol{k}\right\rangle\right]}{\left(\epsilon_{n \boldsymbol{k}}-\epsilon_{m \boldsymbol{k}}\right)^{2}-(\hbar \omega+i \eta)^{2}}
$$

![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404151626119.png)

![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404151704723.png)

# 三、能算什么？

## 1. 自旋霍尔电导的大小
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404152140377.png)

## 2. 自旋霍尔电导与高对称路径的表示图
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404152141191.png)

## 3. 自旋霍尔电导在第一布里渊区的分布图
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202404152141849.png)
