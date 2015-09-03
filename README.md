# General-Knowledge-of-Stochastic-Processes

以下所有内容整理自随即过程与概率论笔记。本文旨在帮助准备电子系推研面试的同学大体复习随机过程的最基本常识，面试中张颢老师的难题深不可测，本文不予关注。

##随机过程
随机过程X(ω,t)是一个二元函数，ω∈Ω(样本空间)，t∈R/+ .t可以指时间(一维)也可以指空间(n维)。
随机过程描述的是一组r.v.(random variable,随机变量)的性质，这些r.v.在同一个样本空间Ω中。
####相关知识
1. X(ω,t)固定t，得到一维分布(单个r.v.)；固定ω，得到样本轨道(sample path)。
2. r.v.之间的关系课上提到3种，相关(Correlation)，马尔科夫性(markov Property)，鞅(Martingale)。


##宽平稳(Wide Sense Stationary, w.s.s.)
1. E[ X(t) ] = mx   (期望是常数)
2. ∀T ∈ R, R<sub>x</sub> (t+T, s+T) = R<sub>x</sub> (t, s) = R<sub>x</sub> (τ)   (τ = t-s) (只取决于相对位置)
####相关知识 (下面讨论的X(t)无特殊说明均为w.s.s.)
1. X(t)与三角级数之间对应，宽平稳随机过程本质上就是三角函数。三角函数(单频)通过LTI系统频率不变，故宽平稳过程通过LTI后仍是宽平稳。


##周期平稳(Cyclostationary) (又叫“循环平稳”)
∃D ∈ R, R<sub>x</sub> (t+D, s+D) = R<sub>x</sub> (t, s)  (与宽平稳有本质区别)
####相关知识 (下面讨论的X(t)无特殊说明均为周期平稳)
1. 循环平稳过程，将相位随机化(随即扰动)之后变为宽平稳。
如，X(t)是循环平稳(周期为D)，构造Y(t) = X(t + θ), θ ~ U(0,D), θ与X独立，则Y(t)是w.s.s.

2. 主流的调制方式BPSK, QPSK , QAM等理论上都是周期平稳的。因为周期平稳加上随机的相位扰动变为宽平稳，故可以将实际中的通信信号视为宽平稳。


##功率谱(Power Spectral Density, PSD)
S<sub>x</sub>(ω) = FT[ R<sub>x</sub>(τ) ] （数学化定义），物理定义是随机过程傅立叶变换在周期上的积分的平方再除以周期T。
####相关知识
1. 维纳钦欣关系(Wiener-Khinchine Relation)：PSD的数学化定义与物理化定义等价

2. PSD是功率P关于频率ω的函数，所以量纲是焦耳(J)

3. 功率谱密度是相关函数的傅立叶变换， S<sub>x</sub>(ω) = FT[ R<sub>x</sub>(τ) ]

##特征函数
Φ<sub>x</sub>(ω) = E [ exp(j  ω<sup>T</sup>  X) ]
####相关知识
1. 对于多维Gauss过程，特征函数尤为重要，因为联合分布式子中有矩阵求逆，计算复杂度高，但特征函数计算复杂度低。

2. Φ<sub>x</sub>(ω) = FT [ f<sub>X</sub>(x) ]

##母函数 (“矩母函数”)
G<sub>x</sub>(z) = E(z<sup>x</sup>) = Σ<sub>k</sub> P(X = k) * z<sup>k</sup>

定义类似z变换。研究Poisson过程时常用母函数做工具。

##高斯过程
随机过程X(t), ∀n, ∀t1, t2, ..., tn, ( X(t1), X(t2),..., X(tn) ) ~ N. 即，任取n个时刻得到的随机变量符合n元联合Gauss分布
####相关知识
1. 线性性：一组Gauss乘任意矩阵仍是Gauss

2. 分量之间的性质：Gauss的边缘分布为Gauss，但是反之不成立！

3. 条件分布：两个Gauss的条件分布仍是Gauss

##泊淞过程
1. N(0) = 0
2. N(t)是独立增量过程   ∀t1<t2≤t3<t4, [N(t2) - N(t1)] 与 [N(t4) - N(t3)] 相互独立
3. 稀疏性   以极限的形式定义了稀疏性：已知在某段时间内事件发生的次数为1，则在同样的时间段内事件发生次数大于等于2的条件概率趋近于0(当时间段长度趋近于0时)
4. N(t)是平稳增量过程    ∀t2>t1, [N(t2) - N(t1)] = f(t2 - t1)  (增量仅取决于时间差) 所以有: N(t+s) - N(t) = N(s) - N(0) = N(s)

定义域与值域: N(t) ∈ N, t∈R, t≥0 (“计数过程”，取值只能是自然数)
####相关知识
1. Poisson过程与Poisson分布的： P( N(t) = k) = [(λt)<sup>k</sup>/k!] * exp(-λt), 满足Poisson分布的形式

2. E[ N(t) ] = λt, Var[ N(t) ] =λt

3. λ称为“强度”，单位时间内事件发生的平均次数

4. Poisson过程的和仍为Poisson

####泊淞过程的推广
1. 非齐次Poisson (也叫“非平稳”)
去掉了平稳增量的要求

2. 复合Poisson  去掉了稀疏性的要求
复合Poisson考察的是不同事件发生造成的影响不同，每次事件发生带来的影响不都记为1. 标准Possion的差是复合Poisson.

3. 过滤Poisson
事件发生后的影响是关于t的函数，可以理解为标记事件发生时间的冲激串通过冲激响应为h的滤波器

##马尔可夫链 (Markov Chains)

##主成份

##一些其他的结论
1. 发射功率受限，给定信道上要更好地传输信号，应让信号X的分布与噪声N的分布一致

2. I，Q两路正交的信号均是高斯的，合起来的复信号幅度是瑞利(Rayleigh)的，相位是均匀的

3. 灌水(Water-filling)的思想：高斯平行信道上传输信号，总的发射功率受限，每个信道的噪声功率不同，要想更好地传输应该在噪声功率越小的信道上分配的发射功率越大。求导可知，最优时P<sub>N</sub> +P<sub>X</sub> = C

4. 