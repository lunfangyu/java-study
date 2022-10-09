# java-study
## 功能说明
做这个多线程异步任务，主要是因为我们有很多永动的异步任务，什么是永动呢？就是任务跑起来后，需要一直跑下去。
比如消息 Push 任务，因为一直有消息过来，所以需要一直去消费 DB 中的未推送消息，就需要整一个 Push 的永动异步任务。

### 我们的需求其实不难，简单总结一下：
1. 能同时执行多个永动的异步任务；
2. 每个异步任务，支持开多个线程去消费这个任务的数据；
3. 支持永动异步任务的优雅关闭，即关闭后，需要把所有的数据消费完毕后，再关闭。

### 完成上面的需求，需要注意几个点：
1. 每个永动任务，可以开一个线程去执行；
2. 每个子任务，因为需要支持并发，需要用线程池控制；
3. 永动任务的关闭，需要通知子任务的并发线程，并支持永动任务和并发子任务的优雅关闭。
