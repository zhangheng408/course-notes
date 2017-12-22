1. errors
  1. 硬错误：组件死亡
  2. 软错误：信号或位错误
  3. 可用性=不失败的时间/总时间=不失败的时间/(不失败的时间+修复所需时间)
    1. 4个9一年52分钟
    2. 3个9一年8.7小时
  4. 澡盆曲线
  5. 错误恢复
    1. 返回错误结果
    2. 检测错误
      1. 奇偶校验
      2. EDC——Error Detection and Correction(冗余)
      3. 校验和，如TPC/UDP/IP
      4. CRC——Cyclic Redundancy Check
        1. 事先选择r+1位的数字G
        2. 选择R，使得<D,R>可以被G整除
        3. 可以检测所有少于r+1位的错误
        4. R=(D<<r)%G
    3. 纠正错误
      1. 冗余
        1. ECC——Error Correcting Codes,如二维奇偶校验
        2. 副本/投票
      2. 重试
  6. 注意失败之间的相关性，可能降低冗余的价值
2. using multi disks
  1. JBOD——Just a bunch of disks
    1. 独立的多个磁盘
    2. 失败直接丢失数据
  2. 分块
  3. 冗余/副本
  4. 奇偶校验磁盘
  5. 循环奇偶校验磁盘
3. RAID
  1. RAID 0——粗粒度分块，没有冗余
    1. 适用性能和容量重要时，可用性没有提升
  2. RAID 1——镜像各自独立的磁盘
    1. 可用性和写性能重要，容量不重要
  3. RAID 2——细粒度分块+Hamming码纠错
  4. RAID 3——细粒度分块+奇偶磁盘
  5. RAID 4——粗粒度分块+奇偶磁盘
  6. RAID 5——粗粒度分块+循环奇偶块
    1. 适用容量和花费重要或读较多的情形
  7. RAID 6——RAID5+另一个奇偶块
  8. RAID 10——RAID1 + RAID0
4. 估算可用性
  1. MTTF——Mean Time Between Failures
  2. MTTDL——mean time to first disk failure
    1. MTTDL = disk.MTTF / #disks 