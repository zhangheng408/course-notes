* CDN: Content Delivery Network
	* 挑战
		* 在哪里做副本
			* Internet Service Provider接口处建立POP
			* POP——Point-of-Presence
		* 如何做副本
			* 先本地检查缓存，不存在再查源
		* 怎么找到重复内容
		* 多副本间如何选择
			* 最低负载
			* 最好性能
			* 随机
		* 客户怎么直连副本
			* 路由：集群负载均衡
			* 应用：HTTP重定向
			* 命名：DNS
		* 容错和一致性
* 基于DNS的客户路由
	* 内容提供商将域名代理给CDN(DNS中的CNAME类别把)
	* CDN高层次名称服务器选定区域
	* CDN低层次名称服务器在区域内选择服务器
* cache管理
	* HOC: Hot Object Cache
	* 大量随机IO
* 开放问题
	* 和机器学习结合进行优化
	* 数据分析和建模
	* 安全



