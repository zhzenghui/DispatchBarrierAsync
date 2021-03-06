# DispatchBarrierAsync
      一个dispatch barrier 允许在一个并发队列中创建一个同步点。当在并发队列中遇到一个barrier, 他会延迟执行barrier的block,等待所有在barrier之前提交的blocks执行结束。 这时，barrier block自己开始执行。 之后， 队列继续正常的执行操作。     
      调用这个函数总是在barrier block被提交之后立即返回，不会等到block被执行。当barrier block到并发队列的最前端，他不会立即执行。相反，队列会等到所有当前正在执行的blocks结束执行。到这时，barrier才开始自己执行。所有在barrier block之后提交的blocks会等到barrier block结束之后才执行。      
      这里指定的并发队列应该是自己通过dispatch_queue_create函数创建的。如果你传的是一个串行队列或者全局并发队列，这个函数等同于dispatch_async函数。
      通过dispatch_barrier_async函数提交的任务会等它前面的任务执行完才开始，然后它后面的任务必须等它执行完毕才能开始。
      必须使用dispatch_queue_create创建的队列才会达到上面的效果.
