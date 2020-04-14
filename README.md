# NYU-7143-Notes-for-optimization-problems
## Convergence rate
- 虽然optimization问题多用于基础研究，工程使用时有多种python库可供调用，但是了解其原理，一是有助于更好的选择optimization function，二是costumize自己的optimiation function（竞赛中常常用到）。
- 首先看一下这篇[知乎](https://zhuanlan.zhihu.com/p/27644403) ，对Convergence rate有一个大概的理解。
- 在发表optimization方向的论文时，需要尤其注意自己的模型属于哪种Convergence rate，并分析其表现: **_time and iteration count_**。
- _**重点：Convergence rate only tells you how close each iteration gets to the best solution, however, it doesn't tell you how costly(timewise) each iteration is.**_ 解释一下就是，虽然有的optimization算法他Convergence rate很优，即可以几步就收敛到最优解，但是他每一次iteration的cost非常大，比如遍历整个数据集，或计算时间很长等，这就是trade-off，工程实现是需仔细考虑。

## 三种Convergence rate
- Convergence rate：Sublinear < Linear < Quadratic  

> Sublinear：SGD （takes the amount of computations comparable with the total amount of the previous work.）

> Linear: GD  （each new right digit of the answer takes a constant amount of
computations）

> Quadratic: 牛顿  （each iteration doubles the number of right digits in
the answer，but expensive）   

（大家都用过的例子：SGD快，但是收敛效果不一定好，GD慢，但是遍历整个数据集，收敛效果好）


