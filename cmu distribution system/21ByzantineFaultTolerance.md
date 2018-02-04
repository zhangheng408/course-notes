* 术语和背景
	* fail:达不到之前的承诺
	* k fault tolerant: k个组件失败，系统仍可以达到预定标准
	* 很难达成一致(Agreement)，甚至有些时候不可能 
* Byzantine Fault Tolerance (Lamport) 
	* 拜占庭问题
		* n个将军要达成一致，其中有一些叛徒
			* 假设了恶意节点
			* 而一般的情景下，节点只会失去响应，而不是变坏
		* 不同于主从模型(一个将军，多个上尉)
	* Traditional replicated state machine (RSM)
		* A RSM w/ 2f+1 replicas can tolerate f simultaneous crashes
			* 是指之前的paxos协议吗？
	* 	为什么RSM不适用拜占庭问题
		*  不能依赖主节点(primary)分配SeqNo，任何节点都可能是恶意的
		*  在paxos中，恶意节点可能同时接受(accept)两个值，造成假象
	*  大部分分布式系统的假设
		*  进程异步
		*  消息单播
		*  通信延时无边界
	*  ByzantineAgreement[Lamport,Shostak,Pease, 1982]
		*  假设：
			*  所有消息正确送达
			*  接收者知道谁发送的消息
			*  消息延时有边界(消息缺失可被检测到)
			*  消息不可被伪造，可被验证（签名机制）
		*  算法
			*  每个进程，将各自的值，发送给其他所有人
			*  每个进程，记录收到的所有值，没收到的设定为默认值
			*  每个进程广播所有值
			*  每个进程获得所有广播结果，并进行计算
		*  之后的签名消息没看懂
			*  一个将军，多个上尉
* Async.BFT(Liskov) 
	* FLP impossibility
		* 分布式系统不能达成异步一致
		* 论文：Impossibility of distributed consensus with one faulty process
	* Practical Byzantine Fault Tolerance
		* 假设
			* 只有一个小部分节点是Byzantine，依赖绝对大多数的投票
			* 做了一些弱同步的假设，不然就会违反FLP不可能性
		* 用3f+1个节点，容忍f个节点错误
		* 主要思想
			* 静态配置
			* 使用三阶段协议达成Seq No一致，解决恶意主节点问题
			* 使用更大的绝对多数2f+1/3f+1（三分之二多数）
			* 需要验证通信
		* 副本状态
			* 副本id为i，从0到N-1
			* v#(view number)从0开始
			* primary就是一个副本包含一个id
			* log <op, seq#, status>
				* status为pre-prepared or prepared or committed
		* 一般流程
			* 客户端先对primary发起请求
			* pre-prepare: primary发起，包含<v#, seq#, op>，防止primary是恶意的
			* prepare: 副本检查收到的消息,广播prepare给所有人，包含<i, v#, seq#, op>
			* commit: 副本等待2f+1个匹配的准备，广播commit，包含<i, v#, seq#, op>
			* Reply: 副本等待2f+1个commit成功，回复客户端
			* 客户端等待f+1个匹配的回复
				* 为啥是f+1了，而不是绝对多数？
				* 假设f个失败，保证至少一个提交了
		* View Change
			* 副本观察主primary
			* 副本广播view change请求
			* 并等待2f+1同意
			* 新主primary发送证明，自己成功了
		* BFT的限制
			* Expensive
			* 无法应对僵尸节点，数据偷盗等(Social Security Number)




