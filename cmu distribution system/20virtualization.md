* 动机
	* 超卖，共享
* 虚拟机
	* IBM/370开始，60~70火，80~90低潮，硬件便宜，OS支持更多
	* 90后期又火
	* 系统虚拟化/进程虚拟化
	* type 1/type 2
	* 经典虚拟化/三要素
	* CPU虚拟化/存储虚拟化/IO虚拟化
	* 完全虚拟化/半虚拟化
* 容器
	* 微服务化，造就容器
		* 计算能力的共享造就容器
	* 和namespace/cgroups/overlayFS结合
	* 某些资源没有隔离，不被内核管理
		* 末级cache(只有一级cache在被管理吧)
		* 存储带宽
	* 可攻击点较多
		* syscall很多，过滤又很难
		* 目前云服务商是VM之上套容器
	* 容器和VM互相补充



