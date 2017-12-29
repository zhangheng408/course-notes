1. Google
  1. Google workqueue(scheduler)
  2. Google File Systerm
  3. Chubby Lock service (paxos-based)
  4. MapReduce
  5. BigTable
  6. Spanner
2. GFS/HDFS
	1. GFS假设
		1. 大文件、流式读写、多客户端并发写(append)
	2. GFS架构
		1. 一个master
			1. Namespace
			2. ACL
			3. 文件到块的映射
			4. 块的位置
			5. 一致性管理
			6. 垃圾回收
			7. 负载均衡
		2. 多个chunk server，64MB文件块，用64bit UID标识
			1. 不缓存数据
			2. 流式读写也没必要缓存
	3. 一致性模式
		1. 命名空间的修改是原子的(只有master)
		2. 修改数据的顺序被master控制
	4. 错容忍
		5. master从磁盘恢复namespace、文件和块的映射
		6. master询问chunk server块信息
		7. chunk server向master发送心跳
		8. chunk server失败后，master会重新复制块
	9. 限制
		10. 没有安全验证，默认安全环境和可信用户
		11. 不会掩饰任何数据失败，需要应用层的校验和
		12. master难以拓展
		13. 文件块比较大
	14. 2010年被Colossus取代
		15. 消除了master单点问题
		16. 考虑了延时敏感应用
		17. 块大小降低到了1-8M
	18. HDFS和GFS很类似
		19. 单写多读模型
		20. 尽量只append；GFS则更多是随机文件写
3. Spanner
	4. 概念
		5. 分布式多版本数据库
		6. 支持通用事务ACID
		7. SQL查询语言
		8. 半(semi)关系型数据模型
	9. 并发控制
		10. 用全局时间戳获取外部一致性
		11. 事务使用严格的2PL
			12. 每个事务T被分配一个时间戳s
			13. 被T修改的数据标记上s
	14. 同步快照
		15. 全局时钟=外部一致性
			16. 提交顺序代表全局时钟顺序
		17. 时间戳顺序==提交顺序
	18. True Time API
		19. TT.now()
			20. 是一个区间表示[earliest, lastest]
		20. TT.before(t)/after(t)
	21. 外部一致性
		22. 两个事务的区间不重合
	24. 总结
		25. 全局一致副本数据库系统
		26. 实现分布式事务
		27. 读无锁，写基于paxos
		28. 通过TrueTime API实现外部一致性
		29. 能够容灾
	30.讲的很粗略

