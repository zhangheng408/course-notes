* Spanner
	* 和上一个课件差不多
	* TrueTime API
		* 客户端和多个GPS time master交互，确地时间
* Naming
	* 名称和对象关联
	* name发现
		* 默认、广播、查询、广播查询等
* Hashing
	* 两大作用：一致性、基于内容的命名
	* 划分问题
		* 静态划分(规则确认)
		* 传统hash
			* bucket = hash(item) / num_buckets 
			* 难以水平拓展
		* 一致性hash
			* key和node都进行hash
			* key找到比自己hash大或相同的第一个node
			* 平滑，且负载均衡
	* 用对象的hash值来命名对象
		* 可以去重
	* hash属性
		* 压缩长度
		* 易于计算
		* Pre-image resistance：不容易通过输出猜到输入
		* 2nd Pre-image resistance：不容易找到另一个输入，输出相同
		* collision resistance：不容易找到两个输入，输出相同
	* Message Authority code
		* H(Key, data)
 




