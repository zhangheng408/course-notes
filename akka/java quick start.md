#### Actor模型

- 事件驱动：终于有人把这个异步管理最好了，我之前觉得不难，为啥没人做？
- 强隔离：Actor之间无共享状态，只能通过事件交互
- 位置透明：可以容灾、负载均衡。factory负责维护Actor生命周期
- 轻量：一个Actor只有几百Byte，应用中可以轻松Million级Actor

#### 定义Actor和消息

- 消息可以是任何类型（Object基类）
- message
  - 命名要好
  - 不可变，因为线程间共享
  - Actor中一般定义一个静态的*props*方法，构建Actor
- Actor只能看到ActorRef
- ActorSystem负责维护Actor生命周期、容灾等
- ActorSystem和Actor都有名字
  - 怎么通过这个名字查找具体的引用？
  - 这些名字确实要求唯一

#### 测试

- 用TestKit做验证
  - new TestKit(system).expectMsgClass(Greeting.class);
  - 来验证消息是否已发送
  - 但是只通过Greeting.class类也获取，是获取当前最新的一个消息？