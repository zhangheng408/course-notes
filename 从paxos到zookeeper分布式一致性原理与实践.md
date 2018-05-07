####分布式架构
* 分布式特点
	* 分布性
	* 对等性
	* 并发性
	* 缺乏全局时钟
	* 故障总会发生
* 分布式环境的问题
	* 通信异常
	* 网络分区
	* 三态：成功、失败、超时
	* 节点故障
* 事务ACID
* CAP理论
	* 分布性系统不能同时满足一致性(Consistency)、可用性(Availability)、分区容错性(Partition tolerance)
	* 如果出现网络分区，保证可用，则一定不一致；保证一致，则不会可用
* BASE理论
	* Basically Available基本可用：失败时允许响应时间的损失或功能的损失
	* Soft State弱状态：允许数据存在中间状态，如正在同步的状态
	* Eventually Consistence最终一致：经过一段时间后，可以达到一致
		* Causal Consistency因果一致：有通信之后，一定保持一致
		* Read your write读己所写：自己不会看到旧值
		* Session Consistency会话一致：同一个会话中，不会看到旧值
		* Monotonic read Consistency单调读一致性：一个进程读取的值，是顺序的
		* Monotonic write Consistency单调写一致：一个进程的写操作顺序执行

####一致性协议
* 2PC
	* 阶段1：协调者询问所有参与节点，参与节点执行并回复
	* 阶段2：协调者发送提交或中断
	* 原理简单，实现方便
	* 同步阻塞，单点问题，数据不一致(阶段二网络分区)，太过保守
* 3PC
	* 阶段1：询问
	* 阶段2：事务预提交/中断
	* 阶段3：提交
	* 减少阻塞范围
* Paxos
	* 选定一个唯一的提案
	* 三种角色：Proposer/Acceptor/Learner

####Paxos的工程实践
* Chubby
  * 谷歌的分布式锁系统
  * 客户端接口类似Unix文件
  * 客户端可以读写Chubby服务器文件，对文件节点加锁，订阅文件变动
  * 用于：GFS/BigTable的Master选举，存储元数据
  * 支持粗粒度的锁
    * 客户端可能持有锁数个小时或几天
    * 一般设计为锁服务宕机后，客户端继续一直持有锁
    * 而细粒度的锁服务宕机后，一般客户端默认释放所有锁
  * 提供事件通知机制
    * 服务器端通知客户端
    * 客户端太多主动轮询效果不好
  * chubby集群一般称为chubby cell
  * 客户端一般通过RPC和服务端通信
  * master选举(paxos协议)
    * 每次选举的master有一定的租期(master lease)
    * 租期到期，或者master宕机后重新选举
  * 读写
    * 读写都给到master
    * 写操作时，master要使用paxos获得多数之后，再响应客户端
    * 读操作时，master自己返回
  * 文件和目录
    * 排他写并不会阻止其他客户端的读请求
    * 锁延时(lock-delay)：避免客户端网络闪断
    * 锁序列器：客户端发送请求时带锁信息，服务器端验证
  * 事件通知机制
    * 文件内容变更
    * 节点删除
    * 子节点新增，删除
    * master服务器转移
  * 缓存
    * master复杂广播失效消息
    * 客户端缓存有一定的租期
  * KeepLive
    * 和心跳类似啊
* Hypertable
  * Master 
  * Hyperspace集群，一个Active Server，多个Standby Server
  * RangeServer
  * DFS Broker
