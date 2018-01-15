* Map/Reduce的限制
	* 每次操作都写入磁盘，90%时间都在IO
	* 延时高，不合适交互型程序
	* 不适合分布式机器学习
* Spark
	* 内存中计算和数据共享：错误容忍
		* RamCloud 多个硬盘支持并发写log，提升性能
		* Resilient Distributed Datasets弹性分布式数据集
			* 使用lineage（感觉就是一个DAG图而已）
			* 粗粒度，失败就重算
			* 不可修改，消耗大量内存，需要很多拷贝
	* 统一的计算和抽象：易用和通用
		* bulk synchronous parallel (BSP)
			* 所有分布式系统抽可以表示为 本地工作 + 消息传输
			* Spark实现了BSP
			* 优化通信
				* 分块
				* no integrity checks (SHA1 is expensive)?
			* 流水线，任务分区减少shuffle
	* Spark不适合的场景
		* 细粒度更新共享状态
		* web应用存储
		* 增量的web爬虫
		* 数据集超过内存
		* 不适合分块batch-analytics的任务
* 分布式机器学习
	* 通信负载
		* 大量机器时，通信也会造成很大性能损耗
		* 没必要所有都通信，有选择的通信
	* BSP出现stragglers拖后腿
		* 没必要每次都全部通信
		* 延时大的可以，等多个周期再同步通信
* BSP为什么不做成DAG图？




