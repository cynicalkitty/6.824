# 6.824
#mapreduce
## 任务分析
### 协调者 coordinator
main/coordiantor 构建并使用协调者
mr/coordinator 存储协调者的构造和功能 
1. 可以读取file作为map task 同时指定reduce task的个数（也就是对多少个key进行统计）
2. 与多个worker进行RPC通信，分配任务
3. 并且需要处理未能及时完成的任务 当任务超过10s 未能完成 需要重新分配，同时要处理可能两个及以上的worker都处理同一任务的情况。***使用Google map reduce中的处理方式，***

### 工作者 worker
main/mrworkder 构建并使用worker 需要并行使用多个worker
mr/worker 待调用的worker工作流程，与coordinator 进行RPC通信，获取任务并执行
###  mapreduce function
main/mrapps/wc 执行word count功能
### RPC
mr/rpc 实现RPC通信
1. worker空闲时向coordinator发起请求 coordinator分配任务给worker
2. worker执行完任务需要向coordinator确认
