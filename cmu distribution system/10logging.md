
1. 错误容忍的动机
    1. Dependability
        1. Availability: 任何时刻都可以服务，随机但很少失败
        2. Reliability: 系统长时间运行不会中断 ，可预测的定期维护，其余时间不失败
        3. Safety: 系统失败不会造成大的灾难
        4. Maintainability：失败之后可以快速修复
    2. Failure model
        1. crash
        2. omission失败：发送/接收
        3. timing时效
        4. response值失败/状态失败
        5. Byzantine失败
    3. Redundancy
        1. 信息冗余 纠错码等
        2. 时间冗余 重做等
        3. 物理冗余 加机器
2. 检查点
    1. 向前恢复: 
    2. 向后恢复: 检查点很贵 
        1. 协调的检查点: 由协调组组织，2PC检查点，请求/确认/提交(放弃) 
3. 日志和恢复
    1. 基本思路：机器失败，磁盘不失败
    2. shadow paging 
        1. 提供原子性和持久性
        2. 写page的时候，有一个对应的外存页面
        3. abort: 直接丢弃影子页
        4. commit: 更新页指针
        5. 避免in-place修改 
    3. write ahead logging
        1. 提供原子性和持久性
        2. 写入磁盘认为可信
        3. 更新version保存在memory中
        4. 通常同时存储Redo/undo 
4. ARIES: Algorithms for Recovery and Isolation Exploiting Semantics
    1.  用在IBM DB2和SQL Server中
    2.  结合WAL/REDO/UNDO
    3.  WAL: 有Log-Sequence Number (LSN)；页级别存储
        1. LSN: [prevLSN, TID, transaction, pageID, new value, ol value] 
    4.  Transaction Table (TT): All TXNS not written to disk
    5.  Dirty Page Table (DPT): all dirty pages in memory
    6.  恢复（3阶段）
        1.   分析: 重建TT和DPT
        2.   redo: 直接向前重复log
        3.   undo: 向后执行log，恢复未提交的内容
    7. 实际中也会和检查点合用，提升性能   