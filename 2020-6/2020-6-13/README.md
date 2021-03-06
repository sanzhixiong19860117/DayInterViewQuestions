# 推箱子自动求解

问：推箱子关卡可以用电脑求解吗？
答：对不太大，箱子不太多的关卡，目前有不少程序都能够求出答案。但是，推箱子已经被数学家和计算机科学家证明 是PSPACE完全(PSPACE-complete)问题，即基本可以认为不存在快速（多项式时间）的求解算法。对于比较大的关卡（如我们MF8推箱子比赛的关卡）， 如今的个人电脑还无能为力。

方法如下：

1. BFS；
2. DFS；
3. A*和IDA*；
4. 遗传算法。

这4种方法，我只用第1种方法，其他方法不熟悉。方法1具体介绍：

1. 拉箱子比推箱子更高效，更有效。原因是拉箱子比起推箱子，天然自带死锁分析，天然自带剪枝功能。
2. 拉箱子和推箱子可以同时进行。拉箱子和推箱子一旦碰头，这就算解决了。经过测试，双向同时进行不一定比只拉箱子高效，原因是推箱子效率不高，太耗时，拖后腿了。
3. 对初始画面进行抽象。画面里有人、箱子、目标、墙、空间、人目标、箱子目标，经过抽象，会有1个起点画面和多个终点画面。起点画面和终点画面里只有箱子、墙、静止空间（人不能去的空间）、运动空间（人可以去的空间）。这样一来，人移动，不会做记录的，只有箱子移动才会做记录。
4. 重复节点过滤。每拉一次或者推一次，都需要保存到缓存。如果缓存里已经有了这个节点，就不需要再保存。
5. 每步节点。对于拉箱子节点，保存当前值和下一步节点，理由是当前节点只有1个下一步节点，而下一步节点有多个当前节点。对于推箱子节点，保存当前值和上一步节点，理由是当前节点只有1个上一步节点，而上一步节点有多个当前节点。
   ⑥死锁分析。死锁分析只针对推箱子。
6. 死锁分析。死锁分析只针对推箱子。