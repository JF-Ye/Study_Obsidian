# 基于 Windows 使用 wannierberri 程序包
## 步骤：
- 将 wannier90 的非自洽步骤产生的 WAVCAR 弄到 windows 本地（自洽的 WAVCAR 不行，此时 wannier90 产生的 WAVCAR 的 K 点数量为 KPOINTS 乘积）
- 在本地文件夹终端运行 `python -m wannierberri.utils.vaspspn` 生成 wannier. spn 文件
- 终端运行 `python -m wannierberri.utils.mmn2uHu wannier90 targets=sHu,sIu` 生成 wannier90.sHu 和 wannier90.sIu 文件

## 参数 ：
### tetra
- tetra=False
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405180927508.png)
- tetra=True
![image.png](https://jf-1325624113.cos.ap-guangzhou.myqcloud.com/study_picture/202405180927784.png)
### adpt_num_iter
- 多次迭代更加精准