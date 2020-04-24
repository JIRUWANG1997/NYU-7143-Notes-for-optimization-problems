-# NYU-7143-Notes-for-optimization-problems
## Convergence rate
- 虽然optimization问题多用于基础研究，工程使用时有多种python库可供调用，但是了解其原理，一是有助于更好的选择optimization function，二是costumize自己的optimiation function（竞赛中常常用到）。
- 课程涉及大量推导，此处不分享相关slide.
- 首先看一下这篇[知乎](https://zhuanlan.zhihu.com/p/27644403) ，对Convergence rate有一个大概的理解。
- 在发表optimization方向的论文时，需要尤其注意自己的模型属于哪种Convergence rate，并分析其表现: **_time and iteration count_**。
- _**重点：Convergence rate only tells you how close each iteration gets to the best solution, however, it doesn't tell you how costly(timewise) each iteration is.**_ 解释一下就是，虽然有的optimization算法他Convergence rate很优秀，即可以几步就收敛到最优解，但是他每一次iteration的cost非常大，比如遍历整个数据集，或计算时间很长等，这就是trade-off，工程实现是需仔细考虑。

## 三种Convergence rate
- Convergence rate：Sublinear < Linear < Quadratic （考）

> Sublinear：SGD （takes the amount of computations comparable with the total amount of the previous work.）

> Linear: GD  （each new right digit of the answer takes a constant amount of
computations）

> Quadratic: 牛顿  （each iteration doubles the number of right digits in
the answer，but expensive）   

（大家都用过的例子：SGD快，但是收敛效果不一定好，GD慢，但是遍历整个数据集，收敛效果好）
例如：你只是一个theoretician，不关心运行时间，你应该选择牛顿optimization，如果你是一个practitioner ，你应该选择DG或SGD。
## optimization算法分析
- (GD，SGD属于first order minimization,只保证收敛到stationary point, 而不保证收敛到local minima。）
### GD----Linear convergence，以GD为例，讲解如何进行更好的optimization。
- 首先我们希望需要去优化的loss function是**strong convex**并且**smooth**的（特别重要），基于这两个条件，可以证明GD算法属于linear convergence(证明见ppt19-21).
（如果GD不可导，则需要使用subgradient代替gradient，此时推导过程基本不变）
- 如果只进行convex假设而不是strong convex，则GD只能是sublinear convergence rate（1/t）.
#### 下面介绍如果并不满足strong convex假设，如何accelerate GD算法: Nesterov's Accelerated GD
- 思想： 每迈出一步，这一步的方向不光是当前的梯度方向，还要加一部分上一步得到的梯度。
- [ ] algorithm：(ppt-26)
- torch.optim.SGD(params, lr=, momentum=0, dampening=0, weight_decay=0, nesterov=False)中使用这个参数，即在发现optimization funcction的convex性不是很好时将nesterov=False置为true，可得到1/t^2的convergence rate，虽然也是sublinear，但是比不加好很多。
- [ ] 源码阅读
- 从另一种证明方法得知，convergence rate反比与hessian矩阵的condition number，即smooth/convex。（strong vonvex:Q,, convex: 根号Q）


