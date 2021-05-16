# 《刚体动力学算法笔记》Chapter2: 空间向量代数(一)

## 空间向量代数(Spatial Vector Algebra)介绍
空间向量结合了刚体的线性运动、转动两个层面。本章主要推导单刚体的空间向量代数表示。

## 数学定义
### 向量和向量空间（Vectors and Vector Spaces）
线性代数中，向量是向量空间的一个元素。本书中常用的四种向量空间如下：
*  <img src="https://www.zhihu.com/equation?tex=R^n" alt="R^n" class="ee_img tr_noresize" eeimg="1"> : 坐标向量空间( coordinate vectors): n个实数的元组，或者 <img src="https://www.zhihu.com/equation?tex=n\times 1" alt="n\times 1" class="ee_img tr_noresize" eeimg="1"> 的矩阵，用于表示其他抽象向量(abstract vector)。
*  <img src="https://www.zhihu.com/equation?tex=E^n" alt="E^n" class="ee_img tr_noresize" eeimg="1"> :欧几里德向量空间( Euclidean vectors):具有大小和方向的欧式空间向量。
*  <img src="https://www.zhihu.com/equation?tex=M^n" alt="M^n" class="ee_img tr_noresize" eeimg="1"> :空间运动向量( spatial motion vectors):描述刚体运动，如速度、加速度
 <img src="https://www.zhihu.com/equation?tex=F^n" alt="F^n" class="ee_img tr_noresize" eeimg="1"> :空间力向量(spatial force vectors):描述刚体受力，如脉冲力、力矩。

空间向量不属于 <img src="https://www.zhihu.com/equation?tex=E^n" alt="E^n" class="ee_img tr_noresize" eeimg="1"> ，而属于 <img src="https://www.zhihu.com/equation?tex=M^n \cup    F^n" alt="M^n \cup    F^n" class="ee_img tr_noresize" eeimg="1"> 。 
*  **命名约定**: 当空间向量和3D向量同时同名出现时，我们使用  <img src="https://www.zhihu.com/equation?tex=\hat{v},\hat{f}" alt="\hat{v},\hat{f}" class="ee_img tr_noresize" eeimg="1"> 来表示空间向量。当坐标向量和抽象向量同时出现时，我们使用 <img src="https://www.zhihu.com/equation?tex=\underline{v}" alt="\underline{v}" class="ee_img tr_noresize" eeimg="1"> 来表示坐标向量。

### 向量对偶空间(ual of a Vector Space)
令 <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> 是一个向量空间。它的对偶 <img src="https://www.zhihu.com/equation?tex=V^*" alt="V^*" class="ee_img tr_noresize" eeimg="1"> 为跟 <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> 维度相同的向量空间，并且含有跟 <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> 的标量乘法(scalar product)定义, <img src="https://www.zhihu.com/equation?tex=u \cdot v" alt="u \cdot v" class="ee_img tr_noresize" eeimg="1">  or  <img src="https://www.zhihu.com/equation?tex=v \cdot u" alt="v \cdot u" class="ee_img tr_noresize" eeimg="1"> 。对偶具有对称性，即如果 <img src="https://www.zhihu.com/equation?tex=U=V^{*}" alt="U=V^{*}" class="ee_img tr_noresize" eeimg="1">  则  <img src="https://www.zhihu.com/equation?tex=V=U^{*}" alt="V=U^{*}" class="ee_img tr_noresize" eeimg="1"> 。 <img src="https://www.zhihu.com/equation?tex=M^n" alt="M^n" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=F^n" alt="F^n" class="ee_img tr_noresize" eeimg="1"> 是对偶的，它们的元素标量乘法 <img src="https://www.zhihu.com/equation?tex=m \cdot f" alt="m \cdot f" class="ee_img tr_noresize" eeimg="1"> 物理上代表了功率。

标量乘法的定义需要满足非奇异性(nondegenerate or nonsingular)， 即如果对于 <img src="https://www.zhihu.com/equation?tex=v \in V" alt="v \in V" class="ee_img tr_noresize" eeimg="1"> ，如果 <img src="https://www.zhihu.com/equation?tex=v \neq 0" alt="v \neq 0" class="ee_img tr_noresize" eeimg="1"> ，则至少存在一个向量 <img src="https://www.zhihu.com/equation?tex=u \in V^{*}" alt="u \in V^{*}" class="ee_img tr_noresize" eeimg="1"> ，满足 <img src="https://www.zhihu.com/equation?tex=v \cdot u \neq 0" alt="v \cdot u \neq 0" class="ee_img tr_noresize" eeimg="1"> 。非奇异性保证了 <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=V^*" alt="V^*" class="ee_img tr_noresize" eeimg="1"> 的对偶基向量一定存在。
### 对偶基(Dual Bases)
假设我们有两个向量空间，  <img src="https://www.zhihu.com/equation?tex=V=U^{*}" alt="V=U^{*}" class="ee_img tr_noresize" eeimg="1"> ，令 <img src="https://www.zhihu.com/equation?tex=\mathcal{D}=\left\{\boldsymbol{d}_{1}, \ldots, \boldsymbol{d}_{n}\right\}" alt="\mathcal{D}=\left\{\boldsymbol{d}_{1}, \ldots, \boldsymbol{d}_{n}\right\}" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=U" alt="U" class="ee_img tr_noresize" eeimg="1"> 的基向量， <img src="https://www.zhihu.com/equation?tex=\mathcal{E}=\left\{\boldsymbol{e}_{1}, \ldots, \boldsymbol{e}_{n}\right\}" alt="\mathcal{E}=\left\{\boldsymbol{e}_{1}, \ldots, \boldsymbol{e}_{n}\right\}" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=V" alt="V" class="ee_img tr_noresize" eeimg="1"> 的基向量。如果它们满足下面互换条件(eciprocity condition)，则构成对偶基(dual basis):

<img src="https://www.zhihu.com/equation?tex=d_{i} \cdot e_{j}=\left\{\begin{array}{ll}
1 & \text { if } i=j \\
0 & \text { otherwise. }
\end{array}\right.
" alt="d_{i} \cdot e_{j}=\left\{\begin{array}{ll}
1 & \text { if } i=j \\
0 & \text { otherwise. }
\end{array}\right.
" class="ee_img tr_noresize" eeimg="1">
一个特殊情况是当 <img src="https://www.zhihu.com/equation?tex=\mathcal{D}=\mathcal{E}" alt="\mathcal{D}=\mathcal{E}" class="ee_img tr_noresize" eeimg="1"> 时，基是正交的，此时 <img src="https://www.zhihu.com/equation?tex=U=V=\mathrm{E}^{n}" alt="U=V=\mathrm{E}^{n}" class="ee_img tr_noresize" eeimg="1"> 。
### 对偶坐标系(Dual Coordinates)
我们使用Plücker坐标系来表示对偶坐标系统。其有一个特定性质:

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{u} \cdot \boldsymbol{v}=\underline{\boldsymbol{u}}^{\mathrm{T}} \underline{\boldsymbol{v}}" alt="\boldsymbol{u} \cdot \boldsymbol{v}=\underline{\boldsymbol{u}}^{\mathrm{T}} \underline{\boldsymbol{v}}" class="ee_img tr_noresize" eeimg="1">
其中 <img src="https://www.zhihu.com/equation?tex=\boldsymbol{u} \in U, \boldsymbol{v} \in V" alt="\boldsymbol{u} \in U, \boldsymbol{v} \in V" class="ee_img tr_noresize" eeimg="1"> 。 <img src="https://www.zhihu.com/equation?tex=\underline{u}" alt="\underline{u}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\underline{v}" alt="\underline{v}" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=u" alt="u" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=v" alt="v" class="ee_img tr_noresize" eeimg="1"> 在对偶坐标系 <img src="https://www.zhihu.com/equation?tex=\mathcal{D}" alt="\mathcal{D}" class="ee_img tr_noresize" eeimg="1">  和  <img src="https://www.zhihu.com/equation?tex=\mathcal{E}" alt="\mathcal{E}" class="ee_img tr_noresize" eeimg="1"> 中的表示。则 <img src="https://www.zhihu.com/equation?tex=\underline{u}" alt="\underline{u}" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=\underline{v}" alt="\underline{v}" class="ee_img tr_noresize" eeimg="1"> 中的每个元素可以表示为:

<img src="https://www.zhihu.com/equation?tex=u_{i}=e_{i} \cdot u \quad ,  \quad v_{i}=d_{i} \cdot v
" alt="u_{i}=e_{i} \cdot u \quad ,  \quad v_{i}=d_{i} \cdot v
" class="ee_img tr_noresize" eeimg="1">
###  <img src="https://www.zhihu.com/equation?tex=a\cdot" alt="a\cdot" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=a \times" alt="a \times" class="ee_img tr_noresize" eeimg="1"> 运算符
可以将 <img src="https://www.zhihu.com/equation?tex=a \cdot " alt="a \cdot " class="ee_img tr_noresize" eeimg="1">  看做 <img src="https://www.zhihu.com/equation?tex=a \cdot b" alt="a \cdot b" class="ee_img tr_noresize" eeimg="1"> 中对b的运算操作， <img src="https://www.zhihu.com/equation?tex=a \cdot" alt="a \cdot" class="ee_img tr_noresize" eeimg="1"> 将 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 映射到标量 <img src="https://www.zhihu.com/equation?tex=a \cdot b" alt="a \cdot b" class="ee_img tr_noresize" eeimg="1"> ，  <img src="https://www.zhihu.com/equation?tex=a \times b" alt="a \times b" class="ee_img tr_noresize" eeimg="1"> 将 <img src="https://www.zhihu.com/equation?tex=b" alt="b" class="ee_img tr_noresize" eeimg="1"> 映射到 <img src="https://www.zhihu.com/equation?tex=a \times b" alt="a \times b" class="ee_img tr_noresize" eeimg="1"> 。下表中列出了一些运算性质，其中 <img src="https://www.zhihu.com/equation?tex=a \times ^*" alt="a \times ^*" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=a \times" alt="a \times" class="ee_img tr_noresize" eeimg="1"> 的对偶运算。

<img src="https://www.zhihu.com/equation?tex=\begin{array}{l}
\boldsymbol{v} \times^{*}=-\boldsymbol{v} \times{ }^{T}\\
(\lambda \boldsymbol{v}) \times=\lambda(\boldsymbol{v} \times) \quad(\lambda \boldsymbol{v}) \times^{*}=\lambda\left(\boldsymbol{v} \times^{*}\right) \quad (\lambda \text { is a scalar) }\\
(\boldsymbol{u}+\boldsymbol{v}) \times=\boldsymbol{u} \times+\boldsymbol{v} \times \quad(\boldsymbol{u}+\boldsymbol{v}) \times^{*}=\boldsymbol{u} \times^{*}+\boldsymbol{v} \times^{*}\\
(\boldsymbol{X} \boldsymbol{v}) \times=\boldsymbol{X} \boldsymbol{v} \times \boldsymbol{X}^{-1} \quad(\boldsymbol{X} \boldsymbol{v}) \times^{*}=\boldsymbol{X}^{*} \boldsymbol{v} \times^{*}\left(\boldsymbol{X}^{*}\right)^{-1} \quad \text { (Plücker transform) }\\
u \times v=-v \times u\\
(\boldsymbol{u} \times \boldsymbol{v}) \cdot=-\boldsymbol{v} \cdot \boldsymbol{u} \times^{*} \quad\left(\boldsymbol{u} \times{ }^{*} \boldsymbol{f}\right) \cdot=-\boldsymbol{f} \cdot \boldsymbol{u} \times\\
(u \times v) \times=u \times v \times-v \times u \times \quad(u \times v) \times^{*}=u \times^{*} v \times^{*}-v \times^{*} u \times^{*}
\end{array}
" alt="\begin{array}{l}
\boldsymbol{v} \times^{*}=-\boldsymbol{v} \times{ }^{T}\\
(\lambda \boldsymbol{v}) \times=\lambda(\boldsymbol{v} \times) \quad(\lambda \boldsymbol{v}) \times^{*}=\lambda\left(\boldsymbol{v} \times^{*}\right) \quad (\lambda \text { is a scalar) }\\
(\boldsymbol{u}+\boldsymbol{v}) \times=\boldsymbol{u} \times+\boldsymbol{v} \times \quad(\boldsymbol{u}+\boldsymbol{v}) \times^{*}=\boldsymbol{u} \times^{*}+\boldsymbol{v} \times^{*}\\
(\boldsymbol{X} \boldsymbol{v}) \times=\boldsymbol{X} \boldsymbol{v} \times \boldsymbol{X}^{-1} \quad(\boldsymbol{X} \boldsymbol{v}) \times^{*}=\boldsymbol{X}^{*} \boldsymbol{v} \times^{*}\left(\boldsymbol{X}^{*}\right)^{-1} \quad \text { (Plücker transform) }\\
u \times v=-v \times u\\
(\boldsymbol{u} \times \boldsymbol{v}) \cdot=-\boldsymbol{v} \cdot \boldsymbol{u} \times^{*} \quad\left(\boldsymbol{u} \times{ }^{*} \boldsymbol{f}\right) \cdot=-\boldsymbol{f} \cdot \boldsymbol{u} \times\\
(u \times v) \times=u \times v \times-v \times u \times \quad(u \times v) \times^{*}=u \times^{*} v \times^{*}-v \times^{*} u \times^{*}
\end{array}
" class="ee_img tr_noresize" eeimg="1">
### 双积( Dyads and Dyadics)
 <img src="https://www.zhihu.com/equation?tex=a b\cdot" alt="a b\cdot" class="ee_img tr_noresize" eeimg="1"> 叫做dyad，是从向量到向量的线性映射,如将 <img src="https://www.zhihu.com/equation?tex=c" alt="c" class="ee_img tr_noresize" eeimg="1"> 映射到 <img src="https://www.zhihu.com/equation?tex=a(b \cdot c)" alt="a(b \cdot c)" class="ee_img tr_noresize" eeimg="1"> 。
dyadic是向量的线性映射。任何dyadic可以表达为dyads的线性和,可以应用于空间惯性张量。

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{L}=\sum_{i=1}^{r} \boldsymbol{a}_{i} \boldsymbol{b}_{i}
" alt="\boldsymbol{L}=\sum_{i=1}^{r} \boldsymbol{a}_{i} \boldsymbol{b}_{i}
" class="ee_img tr_noresize" eeimg="1">
## 空间速度
对于任一空间点P，其速度可以表示为:

<img src="https://www.zhihu.com/equation?tex=v_{P}=v_{O}+\omega \times \overrightarrow{O P}
" alt="v_{P}=v_{O}+\omega \times \overrightarrow{O P}
" class="ee_img tr_noresize" eeimg="1">
其中 <img src="https://www.zhihu.com/equation?tex=O" alt="O" class="ee_img tr_noresize" eeimg="1"> 是刚体 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 上选定点。我们建立笛卡尔坐标系 <img src="https://www.zhihu.com/equation?tex=O_{xyz}" alt="O_{xyz}" class="ee_img tr_noresize" eeimg="1"> ，定义其正交基为: <img src="https://www.zhihu.com/equation?tex=\{\boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k}\} \subset \mathrm{E}^{3}" alt="\{\boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k}\} \subset \mathrm{E}^{3}" class="ee_img tr_noresize" eeimg="1"> ,则角速度 <img src="https://www.zhihu.com/equation?tex=\omega" alt="\omega" class="ee_img tr_noresize" eeimg="1"> 和线速度 <img src="https://www.zhihu.com/equation?tex=v_O" alt="v_O" class="ee_img tr_noresize" eeimg="1"> 可以表示为:

<img src="https://www.zhihu.com/equation?tex=\omega=\omega_{x} i+\omega_{y} j+\omega_{z} k \quad, \quad \boldsymbol{v}_{O}=v_{O x} \boldsymbol{i}+v_{O y} j+v_{O z} \boldsymbol{k}" alt="\omega=\omega_{x} i+\omega_{y} j+\omega_{z} k \quad, \quad \boldsymbol{v}_{O}=v_{O x} \boldsymbol{i}+v_{O y} j+v_{O z} \boldsymbol{k}" class="ee_img tr_noresize" eeimg="1">
我们的目标是得到表示相同运动的空间速度向量 <img src="https://www.zhihu.com/equation?tex=\hat{\boldsymbol{v}} \in \mathrm{M}^{6}" alt="\hat{\boldsymbol{v}} \in \mathrm{M}^{6}" class="ee_img tr_noresize" eeimg="1"> 。首先定义 <img src="https://www.zhihu.com/equation?tex=M^6" alt="M^6" class="ee_img tr_noresize" eeimg="1"> 上的基:
 <img src="https://www.zhihu.com/equation?tex=\mathcal{D}_{O}=\left\{\boldsymbol{d}_{O x}, \boldsymbol{d}_{O y}, \boldsymbol{d}_{O z}, \boldsymbol{d}_{x}, \boldsymbol{d}_{y}, \boldsymbol{d}_{z}\right\} \subset \mathrm{M}^{6}" alt="\mathcal{D}_{O}=\left\{\boldsymbol{d}_{O x}, \boldsymbol{d}_{O y}, \boldsymbol{d}_{O z}, \boldsymbol{d}_{x}, \boldsymbol{d}_{y}, \boldsymbol{d}_{z}\right\} \subset \mathrm{M}^{6}" class="ee_img tr_noresize" eeimg="1"> ,如图所示，其中 <img src="https://www.zhihu.com/equation?tex=d_{O x}、d_{O y}、d_{O z}" alt="d_{O x}、d_{O y}、d_{O z}" class="ee_img tr_noresize" eeimg="1"> 是绕 <img src="https://www.zhihu.com/equation?tex=O_x,O_y,O_z" alt="O_x,O_y,O_z" class="ee_img tr_noresize" eeimg="1"> 的单位旋转。因此可得：
![空间速度坐标系](./2.1.jpg)

<img src="https://www.zhihu.com/equation?tex=\hat{v}=\omega_{x} d_{O x}+\omega_{y} d_{O y}+\omega_{z} d_{O z}+v_{O x} d_{x}+v_{O y} d_{y}+v_{O z} d_{z}
" alt="\hat{v}=\omega_{x} d_{O x}+\omega_{y} d_{O y}+\omega_{z} d_{O z}+v_{O x} d_{x}+v_{O y} d_{y}+v_{O z} d_{z}
" class="ee_img tr_noresize" eeimg="1">
在 <img src="https://www.zhihu.com/equation?tex=\mathcal{D}_{O}" alt="\mathcal{D}_{O}" class="ee_img tr_noresize" eeimg="1"> 坐标系中可以表达为:

<img src="https://www.zhihu.com/equation?tex=\hat{\underline{v}}_{O}=\left[\begin{array}{c}
\omega_{x} \\
\omega_{y} \\
\omega_{z} \\
v_{O x} \\
v_{O y} \\
v_{O z}
\end{array}\right]=\left[\begin{array}{c}
\underline{\boldsymbol{\omega}} \\
\underline{\boldsymbol{v}}_{O}
\end{array}\right]
" alt="\hat{\underline{v}}_{O}=\left[\begin{array}{c}
\omega_{x} \\
\omega_{y} \\
\omega_{z} \\
v_{O x} \\
v_{O y} \\
v_{O z}
\end{array}\right]=\left[\begin{array}{c}
\underline{\boldsymbol{\omega}} \\
\underline{\boldsymbol{v}}_{O}
\end{array}\right]
" class="ee_img tr_noresize" eeimg="1">

虽然上式中选择固定点 <img src="https://www.zhihu.com/equation?tex=O" alt="O" class="ee_img tr_noresize" eeimg="1"> ，可以证明空间向量跟选择的坐标原点无关。这里我们定义点 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 为原点，对应的速度为 <img src="https://www.zhihu.com/equation?tex=\hat{v}^{\prime}" alt="\hat{v}^{\prime}" class="ee_img tr_noresize" eeimg="1"> 。而 <img src="https://www.zhihu.com/equation?tex=\hat{v}^{\prime}=\hat{v}" alt="\hat{v}^{\prime}=\hat{v}" class="ee_img tr_noresize" eeimg="1"> 。因此 <img src="https://www.zhihu.com/equation?tex=\hat{v}^{\prime}" alt="\hat{v}^{\prime}" class="ee_img tr_noresize" eeimg="1"> 可以表达为:

<img src="https://www.zhihu.com/equation?tex=\hat{\boldsymbol{v}}^{\prime}=\omega_{x} \boldsymbol{d}_{P x}+\omega_{y} \boldsymbol{d}_{P y}+\omega_{z} \boldsymbol{d}_{P z}+v_{P x} \boldsymbol{d}_{x}+v_{P y} \boldsymbol{d}_{y}+v_{P z} \boldsymbol{d}_{z} \tag{1}
" alt="\hat{\boldsymbol{v}}^{\prime}=\omega_{x} \boldsymbol{d}_{P x}+\omega_{y} \boldsymbol{d}_{P y}+\omega_{z} \boldsymbol{d}_{P z}+v_{P x} \boldsymbol{d}_{x}+v_{P y} \boldsymbol{d}_{y}+v_{P z} \boldsymbol{d}_{z} \tag{1}
" class="ee_img tr_noresize" eeimg="1">
不妨选择 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 在 <img src="https://www.zhihu.com/equation?tex=O_{xyz}" alt="O_{xyz}" class="ee_img tr_noresize" eeimg="1"> 中的位置是 <img src="https://www.zhihu.com/equation?tex=(r,0,0)" alt="(r,0,0)" class="ee_img tr_noresize" eeimg="1"> ，如下图所示。此时在 <img src="https://www.zhihu.com/equation?tex=O_{xyz}" alt="O_{xyz}" class="ee_img tr_noresize" eeimg="1"> 坐标系下的线速度为:
![原点无关性](./2.2.jpg)

<img src="https://www.zhihu.com/equation?tex=\left[\begin{array}{l}
v_{P x} \\
v_{P y} \\
v_{P z}
\end{array}\right]=\underline{v}_{O}+\underline{\omega} \times\left[\begin{array}{l}
r \\
0 \\
0
\end{array}\right]=\left[\begin{array}{c}
v_{O x} \\
v_{O y}+\omega_{z} r \\
v_{O z}-\omega_{y} r
\end{array}\right]
" alt="\left[\begin{array}{l}
v_{P x} \\
v_{P y} \\
v_{P z}
\end{array}\right]=\underline{v}_{O}+\underline{\omega} \times\left[\begin{array}{l}
r \\
0 \\
0
\end{array}\right]=\left[\begin{array}{c}
v_{O x} \\
v_{O y}+\omega_{z} r \\
v_{O z}-\omega_{y} r
\end{array}\right]
" class="ee_img tr_noresize" eeimg="1">
另外，在新坐标系 <img src="https://www.zhihu.com/equation?tex=P_{xyz}" alt="P_{xyz}" class="ee_img tr_noresize" eeimg="1"> 下的基向量为:

<img src="https://www.zhihu.com/equation?tex=\begin{array}{l}
d_{P x}=d_{O x} \\
d_{P y}=d_{O y}+r d_{z} \\
d_{P z}=d_{O z}-r d_{y} .
\end{array}
" alt="\begin{array}{l}
d_{P x}=d_{O x} \\
d_{P y}=d_{O y}+r d_{z} \\
d_{P z}=d_{O z}-r d_{y} .
\end{array}
" class="ee_img tr_noresize" eeimg="1">
可得:

<img src="https://www.zhihu.com/equation?tex=\begin{aligned}
\hat{\boldsymbol{v}}^{\prime}=& \omega_{x} \boldsymbol{d}_{O x}+\omega_{y}\left(\boldsymbol{d}_{O y}+r \boldsymbol{d}_{z}\right)+\omega_{z}\left(\boldsymbol{d}_{O z}-r \boldsymbol{d}_{y}\right) \\
&+v_{O x} \boldsymbol{d}_{x}+\left(v_{O y}+\omega_{z} r\right) d_{y}+\left(v_{O z}-\omega_{y} r\right) d_{z}
\end{aligned}
" alt="\begin{aligned}
\hat{\boldsymbol{v}}^{\prime}=& \omega_{x} \boldsymbol{d}_{O x}+\omega_{y}\left(\boldsymbol{d}_{O y}+r \boldsymbol{d}_{z}\right)+\omega_{z}\left(\boldsymbol{d}_{O z}-r \boldsymbol{d}_{y}\right) \\
&+v_{O x} \boldsymbol{d}_{x}+\left(v_{O y}+\omega_{z} r\right) d_{y}+\left(v_{O z}-\omega_{y} r\right) d_{z}
\end{aligned}
" class="ee_img tr_noresize" eeimg="1">
跟 <img src="https://www.zhihu.com/equation?tex=O_{xyz}" alt="O_{xyz}" class="ee_img tr_noresize" eeimg="1"> 的坐标表达公式(1)相同。
## 空间力
作用在刚体 <img src="https://www.zhihu.com/equation?tex=B" alt="B" class="ee_img tr_noresize" eeimg="1"> 上的广义力由一个通过原点 <img src="https://www.zhihu.com/equation?tex=O" alt="O" class="ee_img tr_noresize" eeimg="1"> 的线性力 <img src="https://www.zhihu.com/equation?tex=f" alt="f" class="ee_img tr_noresize" eeimg="1"> 和一个力偶 <img src="https://www.zhihu.com/equation?tex=n_O" alt="n_O" class="ee_img tr_noresize" eeimg="1"> 组成。同理，我们可以计算任一点 <img src="https://www.zhihu.com/equation?tex=P" alt="P" class="ee_img tr_noresize" eeimg="1"> 的总力矩为:

<img src="https://www.zhihu.com/equation?tex=n_{P}=n_{O}+f \times \overrightarrow{O P}
" alt="n_{P}=n_{O}+f \times \overrightarrow{O P}
" class="ee_img tr_noresize" eeimg="1">
引入笛卡尔坐标系 <img src="https://www.zhihu.com/equation?tex=O_{xyz}" alt="O_{xyz}" class="ee_img tr_noresize" eeimg="1"> ，其正交基 <img src="https://www.zhihu.com/equation?tex=\{\boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k}\} \in \mathrm{E}^{3}" alt="\{\boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k}\} \in \mathrm{E}^{3}" class="ee_img tr_noresize" eeimg="1"> 。则 <img src="https://www.zhihu.com/equation?tex=n_O" alt="n_O" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=f" alt="f" class="ee_img tr_noresize" eeimg="1"> 在笛卡尔坐标下的表示为:

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{n}_{O}=n_{O x} \boldsymbol{i}+n_{O y} \boldsymbol{j}+n_{O z} \boldsymbol{k} \quad ,\quad f=f_{x} i+f_{y} j+f_{z} k
" alt="\boldsymbol{n}_{O}=n_{O x} \boldsymbol{i}+n_{O y} \boldsymbol{j}+n_{O z} \boldsymbol{k} \quad ,\quad f=f_{x} i+f_{y} j+f_{z} k
" class="ee_img tr_noresize" eeimg="1">
这个坐标系也定义了 <img src="https://www.zhihu.com/equation?tex=F^6" alt="F^6" class="ee_img tr_noresize" eeimg="1"> 上的Plücker基 <img src="https://www.zhihu.com/equation?tex=\mathcal{E}_{O}=\left\{\boldsymbol{e}_{x}, \boldsymbol{e}_{y}, \boldsymbol{e}_{z}, \boldsymbol{e}_{O x}, e_{O y}, e_{O z}\right\} \subset \mathrm{F}^{6}" alt="\mathcal{E}_{O}=\left\{\boldsymbol{e}_{x}, \boldsymbol{e}_{y}, \boldsymbol{e}_{z}, \boldsymbol{e}_{O x}, e_{O y}, e_{O z}\right\} \subset \mathrm{F}^{6}" class="ee_img tr_noresize" eeimg="1"> 
![空间力坐标系](./2.3.jpg)
同理，如果 <img src="https://www.zhihu.com/equation?tex=\hat{f} \in \mathrm{F}^{6}" alt="\hat{f} \in \mathrm{F}^{6}" class="ee_img tr_noresize" eeimg="1"> 是同样的空间力，则:

<img src="https://www.zhihu.com/equation?tex=\hat{f}=n_{O x} e_{x}+n_{O y} e_{y}+n_{O z} e_{z}+f_{x} e_{O x}+f_{y} e_{O y}+f_{z} e_{O z}
" alt="\hat{f}=n_{O x} e_{x}+n_{O y} e_{y}+n_{O z} e_{z}+f_{x} e_{O x}+f_{y} e_{O y}+f_{z} e_{O z}
" class="ee_img tr_noresize" eeimg="1">
在 <img src="https://www.zhihu.com/equation?tex=\mathcal{E}_{O}" alt="\mathcal{E}_{O}" class="ee_img tr_noresize" eeimg="1"> 坐标系下的表示为:

<img src="https://www.zhihu.com/equation?tex=\underline{\hat{f}}_{O}=\left[\begin{array}{c}
n_{O x} \\
n_{O y} \\
n_{O z} \\
f_{x} \\
f_{y} \\
f_{z}
\end{array}\right]=\left[\begin{array}{c}
\underline{n}_{O} \\
\underline{f}
\end{array}\right]
" alt="\underline{\hat{f}}_{O}=\left[\begin{array}{c}
n_{O x} \\
n_{O y} \\
n_{O z} \\
f_{x} \\
f_{y} \\
f_{z}
\end{array}\right]=\left[\begin{array}{c}
\underline{n}_{O} \\
\underline{f}
\end{array}\right]
" class="ee_img tr_noresize" eeimg="1">
## 线向量和自由向量(Line Vectors and Free Vectors)
线向量是由带方向的线和大小决定的量，比如刚体纯旋转、线性作用力是线向量。自由向量是由方向和大小决定的量，比如刚体位移、力矩作用。一个线向量可以由一个自由向量和线上的任一点确定。

设 <img src="https://www.zhihu.com/equation?tex=\hat{s}" alt="\hat{s}" class="ee_img tr_noresize" eeimg="1"> 是一个代表运动或者力的空间向量，在Plücker坐标系下由 <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=s_O" alt="s_O" class="ee_img tr_noresize" eeimg="1"> 两个3D坐标向量组成。则:
* 如果 <img src="https://www.zhihu.com/equation?tex=s=0" alt="s=0" class="ee_img tr_noresize" eeimg="1"> ,则 <img src="https://www.zhihu.com/equation?tex=\hat{s}" alt="\hat{s}" class="ee_img tr_noresize" eeimg="1"> 是自由向量。
* 如果 <img src="https://www.zhihu.com/equation?tex=s \cdot s_O=0" alt="s \cdot s_O=0" class="ee_img tr_noresize" eeimg="1"> 则 <img src="https://www.zhihu.com/equation?tex=\hat{s}" alt="\hat{s}" class="ee_img tr_noresize" eeimg="1"> 是线向量。线方向由 <img src="https://www.zhihu.com/equation?tex=s" alt="s" class="ee_img tr_noresize" eeimg="1"> 给定，线上的点满足 <img src="https://www.zhihu.com/equation?tex=\overrightarrow{O P} \times s=s_{O}" alt="\overrightarrow{O P} \times s=s_{O}" class="ee_img tr_noresize" eeimg="1"> 。
* 任何空间向量可以表示为线向量和自由向量的和。
* 任何不是自由向量的空间向量，可以如下唯一表示为线向量和平行的自由向量的和，即可以表示为一条带方向的线+线性方向的大小+角度朝向的大小。

<img src="https://www.zhihu.com/equation?tex=\left[\begin{array}{c}
s \\
s_{O}-h s
\end{array}\right]+\left[\begin{array}{c}
0 \\
h s
\end{array}\right] \quad \text { where } \quad h=\frac{s \cdot s_{O}}{s \cdot s}
" alt="\left[\begin{array}{c}
s \\
s_{O}-h s
\end{array}\right]+\left[\begin{array}{c}
0 \\
h s
\end{array}\right] \quad \text { where } \quad h=\frac{s \cdot s_{O}}{s \cdot s}
" class="ee_img tr_noresize" eeimg="1">
根据旋量理论，刚体运动可以标表示为绕空间轴线的旋转和沿着轴线的位移，称为twist；作用在刚体上的广义力可以表示为一个线性力和沿着力方向的力矩,成为wrench，分别对应 <img src="https://www.zhihu.com/equation?tex=M^6" alt="M^6" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=F^6" alt="F^6" class="ee_img tr_noresize" eeimg="1"> 上的元素。

## 标量乘积(Scalar Product)
标量乘积构成了 <img src="https://www.zhihu.com/equation?tex=M^6" alt="M^6" class="ee_img tr_noresize" eeimg="1"> 和 <img src="https://www.zhihu.com/equation?tex=F^6" alt="F^6" class="ee_img tr_noresize" eeimg="1"> 空间的对偶联系。这里进一步定义对偶坐标系统的基: <img src="https://www.zhihu.com/equation?tex=\left\{\boldsymbol{d}_{1}, \ldots, \boldsymbol{d}_{6}\right\} \subset \mathrm{M}^{6}" alt="\left\{\boldsymbol{d}_{1}, \ldots, \boldsymbol{d}_{6}\right\} \subset \mathrm{M}^{6}" class="ee_img tr_noresize" eeimg="1">  和  <img src="https://www.zhihu.com/equation?tex=\left\{\boldsymbol{e}_{1}, \ldots, e_{6}\right\} \subset \mathrm{F}^{6}" alt="\left\{\boldsymbol{e}_{1}, \ldots, e_{6}\right\} \subset \mathrm{F}^{6}" class="ee_img tr_noresize" eeimg="1"> ，满足以下关系:

<img src="https://www.zhihu.com/equation?tex=d_{i} \cdot e_{j}=\left\{\begin{array}{ll}
1 & \text { if } i=j \\
0 & \text { otherwise }
\end{array}\right.
" alt="d_{i} \cdot e_{j}=\left\{\begin{array}{ll}
1 & \text { if } i=j \\
0 & \text { otherwise }
\end{array}\right.
" class="ee_img tr_noresize" eeimg="1">
此时，如果一个矩阵 <img src="https://www.zhihu.com/equation?tex=M" alt="M" class="ee_img tr_noresize" eeimg="1"> 代表运动向量的变换， <img src="https://www.zhihu.com/equation?tex=X^*" alt="X^*" class="ee_img tr_noresize" eeimg="1"> 代表力向量的变换，则满足:

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{X}^{*}=\boldsymbol{X}^{-\mathrm{T}}
" alt="\boldsymbol{X}^{*}=\boldsymbol{X}^{-\mathrm{T}}
" class="ee_img tr_noresize" eeimg="1">

## 使用空间向量
空间向量用于表达和分析刚体系统和刚体动力学。这里简单说明其和实际物理系统的联系:
* **用途:** <img src="https://www.zhihu.com/equation?tex=M^6" alt="M^6" class="ee_img tr_noresize" eeimg="1"> 上元素描述刚体运动，如速度、加速度、无限小位移、运动自由度和约束的方向。 <img src="https://www.zhihu.com/equation?tex=F^6" alt="F^6" class="ee_img tr_noresize" eeimg="1"> 上的元素描述作用在刚体上的力，如力矩、脉冲力、力自由度和约束的方向。
* **唯一性:**  <img src="https://www.zhihu.com/equation?tex=M^6" alt="M^6" class="ee_img tr_noresize" eeimg="1"> 上元素和刚体运动1：1映射， <img src="https://www.zhihu.com/equation?tex=F^6" alt="F^6" class="ee_img tr_noresize" eeimg="1"> 同理。
* **相对性:** 如果刚体 <img src="https://www.zhihu.com/equation?tex=B_1,B_2" alt="B_1,B_2" class="ee_img tr_noresize" eeimg="1"> 的速度分别为 <img src="https://www.zhihu.com/equation?tex=v_1,v_2" alt="v_1,v_2" class="ee_img tr_noresize" eeimg="1"> 。 <img src="https://www.zhihu.com/equation?tex=B_2" alt="B_2" class="ee_img tr_noresize" eeimg="1"> 相对 <img src="https://www.zhihu.com/equation?tex=B_1" alt="B_1" class="ee_img tr_noresize" eeimg="1"> 的速度为: <img src="https://www.zhihu.com/equation?tex=\boldsymbol{v}_{r e l}=\boldsymbol{v}_{2}-\boldsymbol{v}_{1}" alt="\boldsymbol{v}_{r e l}=\boldsymbol{v}_{2}-\boldsymbol{v}_{1}" class="ee_img tr_noresize" eeimg="1"> 。相对加速度为 <img src="https://www.zhihu.com/equation?tex=\boldsymbol{a}_{r e l}=\boldsymbol{a}_{2}-\boldsymbol{a}_{1}" alt="\boldsymbol{a}_{r e l}=\boldsymbol{a}_{2}-\boldsymbol{a}_{1}" class="ee_img tr_noresize" eeimg="1"> 。
* **累积性:** 力空间向量可以累加。惯量也可以累积，如果两个刚体固接，整体惯量为: <img src="https://www.zhihu.com/equation?tex=I=I_1+I_2" alt="I=I_1+I_2" class="ee_img tr_noresize" eeimg="1"> 。
* **运动方程:**  <img src="https://www.zhihu.com/equation?tex=\boldsymbol{f}=\mathrm{d} / \mathrm{d} t(\boldsymbol{I} \boldsymbol{v})=\boldsymbol{I} a+\boldsymbol{v} \times^{*} \boldsymbol{I} \boldsymbol{v}" alt="\boldsymbol{f}=\mathrm{d} / \mathrm{d} t(\boldsymbol{I} \boldsymbol{v})=\boldsymbol{I} a+\boldsymbol{v} \times^{*} \boldsymbol{I} \boldsymbol{v}" class="ee_img tr_noresize" eeimg="1"> , 


> 如图所示运动链， <img src="https://www.zhihu.com/equation?tex=v_i" alt="v_i" class="ee_img tr_noresize" eeimg="1"> 代表第i个刚体的速度， <img src="https://www.zhihu.com/equation?tex=v_{Ji}" alt="v_{Ji}" class="ee_img tr_noresize" eeimg="1"> 代表关节i的速度，则:

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{v}_{\mathrm{J} i}=\boldsymbol{v}_{i}-\boldsymbol{v}_{i-1}
" alt="\boldsymbol{v}_{\mathrm{J} i}=\boldsymbol{v}_{i}-\boldsymbol{v}_{i-1}
" class="ee_img tr_noresize" eeimg="1">
> 因为关节只有一个自由度，可以表示成轴向量和速度向量: <img src="https://www.zhihu.com/equation?tex=\boldsymbol{v}_{\mathrm{J} i}=\boldsymbol{s}_{i} \dot{q}_{i}" alt="\boldsymbol{v}_{\mathrm{J} i}=\boldsymbol{s}_{i} \dot{q}_{i}" class="ee_img tr_noresize" eeimg="1"> 。则:

<img src="https://www.zhihu.com/equation?tex=\boldsymbol{v}_{i}=\boldsymbol{v}_{i-1}+\boldsymbol{s}_{i} \dot{q}_{i} =\sum_{j=1}^{i} s_{j} \dot{q}_{j} \quad\left(\boldsymbol{v}_{0}=\mathbf{0}\right)
" alt="\boldsymbol{v}_{i}=\boldsymbol{v}_{i-1}+\boldsymbol{s}_{i} \dot{q}_{i} =\sum_{j=1}^{i} s_{j} \dot{q}_{j} \quad\left(\boldsymbol{v}_{0}=\mathbf{0}\right)
" class="ee_img tr_noresize" eeimg="1">
> 或者可以表示为矩阵形式，其中 <img src="https://www.zhihu.com/equation?tex=J_i" alt="J_i" class="ee_img tr_noresize" eeimg="1"> 是 <img src="https://www.zhihu.com/equation?tex=6 \times N" alt="6 \times N" class="ee_img tr_noresize" eeimg="1"> 的Jacobian， <img src="https://www.zhihu.com/equation?tex=\dot{q}" alt="\dot{q}" class="ee_img tr_noresize" eeimg="1"> 是关节空间速度向量:

<img src="https://www.zhihu.com/equation?tex=v_{i}=\left[\begin{array}{lllllll}
s_{1} & s_{2} & \cdots & s_{i} & 0 & \cdots & 0
\end{array}\right]\left[\begin{array}{c}
\dot{q}_{1} \\
\vdots \\
\dot{q}_{N}
\end{array}\right]=J_{i} \dot{q}
" alt="v_{i}=\left[\begin{array}{lllllll}
s_{1} & s_{2} & \cdots & s_{i} & 0 & \cdots & 0
\end{array}\right]\left[\begin{array}{c}
\dot{q}_{1} \\
\vdots \\
\dot{q}_{N}
\end{array}\right]=J_{i} \dot{q}
" class="ee_img tr_noresize" eeimg="1">
>
> ![example 2.3](2.4.jpg) 