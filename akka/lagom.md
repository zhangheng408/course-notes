#### 服务框架

- 定义服务接口及实现
  - descriptor函数，指定名称、URL、HTTP方法、对应函数实现
  - 返回的是一个Descriptor变量
- url对应函数的实现，返回值是ServiceCall<Type1, Type2>
  - 这个接口定义如下

`interface ServiceCall<Request, Response> {  CompletionStage<Response> invoke(Request request);}`

