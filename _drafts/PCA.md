主成分分析 Principal component analysis (PCA)

### 定义

PCA 是一种统计过程，它使用正交变换，将一系列可能相关的变量的观测转换到另外一系列的线性无关的变量，这些线性无关的变量称为主成分。

主成分分析经常用于减少数据集的维数，同时保持数据集中的对方差贡献最大的特征。这是通过保留低阶主成分，忽略高阶主成分做到的。

PCA 需要找到一个超平面，使得样本点离该超平面距离足够近的同时，又能保证投影点尽可能分开，从而达到降维的目的。

记 $$n$$ 个观测的 $$m$$ 维数据矩阵为 $$X_{m \times n}$$，PCA 的目的是寻找一个变换矩阵 $$P_{d \times m$$, $$d$$ 远小于 $$m$$，则 $$Y = PX$$，即将原始 m 维数据点在 d 维空间表示。

那如何选择这个矩阵呢？假如原数据矩阵在每个特征维度的均值都是 0，即 $$\sum_i{x_i}=0$$，则可知转换后每一维的均值也为 0。考虑矩阵 $$A=\frac{1}{n}X*X^T$$，即原数据的协方差矩阵，协方差矩阵对角线的值即 m 维空间里每一维的方差，非对角线的值则是两个维度之间的协方差。

对于降维之后的协方差矩阵 $$B=\frac{1}{n}Y*Y^T$$，根据上面的分析，我们希望这个矩阵的对角线值尽可能大，即特征方差变大，而非对角线值尽可能小，即协方差矩阵的每一维是正交的，正交会使得两个维度是无关的。

### 步骤

1. 均值
2. 协方差矩阵
3. 奇异值分解？
4. ​

### SVD

https://zealscott.com/blog/linear-algebra-notes-15-svd-decomposition/

https://zhuanlan.zhihu.com/p/36546367

https://zhuanlan.zhihu.com/p/36799949

https://www.zhihu.com/question/38319536

