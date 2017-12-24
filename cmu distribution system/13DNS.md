1. DNS design
  1. DNS设计目标
    1. 广域网分布式数据库
    2. 可拓展
    3. 非中心化
    4. 鲁棒性
    5. 全局一致
    6. 不需要原子性和强一致性
  2. DNS格式
    1. id/flags(是否有下面的域)
    2. 含问题，问题答案(Resource Records)，认证、其他RR等
    3. 每中都是可变的数量
    4. RR格式(class, name, value, type, ttl)
      1. class=Internet (IN), Chaosnet (CH)等
      2. type==A，name是域名，value是ip
      3. type==CNAME，name是别名，value是域名
      4. type==NS，name是域名，value是认真的Name Server
      5. type==MX，name是域名，value是邮件服务器的名称
  3. 层级架构
    1. 13个根Name Server
    2. 通常本地先查缓存、再查local DNS，再查root DNS，再查对应的DNS.
    3. DNS负载均衡
    4. DNS缓存定期超时
2. DNS Today
  1. 防御DDOS攻击
    1. 使用其他的DNS提供者
    2. 降低DNS server的TTL，使客户去向其他服务器