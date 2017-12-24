1. 超级计算机
  1. Traditional high-performance computing (HPC)
    1. 编程模型很底层，依赖较少
  2. 块同步编程Bulk Synchronous Programming
    1. 把程序划分为P个区域，分别给p个处理器执行
    2. 各个处理器之间周期性通信，交流边界条件
  3. 错误恢复——似乎只有检查点
  4. 性能对失败模块非常敏感
2. 集群计算
  1. Data-Intensive系统的挑战
    1. 多硬盘/处理器，千兆以太网连接，分布有局部性
  2. 集群编程模型——比较高层次
  3. MapReduce
    1. 程序员要实现Mapper和Reduce
    2. Mapper每次读入一行，产生<k,v>
    3. Reducer对key迭代
    4. 举例矩阵相乘，先算乘，再加和
  4. Mapping——把输入按key hash为R个文件
  5. Shuffling——R个Reducer，每个取对应的R文件
  6. Reducing——按照key进行reducer
  7. 优劣——高负载，错误容忍，自动调度(掉队者)，没有局部性
  8. 并行计算模型从粗到细
    1. MapReduce/Threads/MPI/PRAM
3. 其他计算框架
  1. Microsoft Dryad Project
    1. operators的DAG图
    2. 每个operator输入一些对象，输出一些对象
    3. 纯函数模型
  2. CMU GraphLab
    1. 把计算视为图节点的更新
    2. 每个图节点只依赖于邻居
    3. 不断更新节点，直到稳定