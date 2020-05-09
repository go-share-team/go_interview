**Go scheduler源码分析**

`https://segmentfault.com/a/1190000018777972`

**Go GMP 流转案例**

`1. time.sleep 阻塞时, time内部由最小堆实现。通过gopark解绑GM`

`2. 网络请求 阻塞,  网络IO 其实就是打开一个socket流。读写数据。将GR被移动到 epoll模型中。不影响当前M和P的绑定执行其他GR`

`3. 调用系统方法 比如文件IO时, GM单继续独自处理阻塞。而M和P解绑。P会切换一个新的M(如果有空闲M 获取空闲M) 绑定后 继续执行其他GR`



**GO 抢占问题**

`1.谁来负责标记抢占? sysmon 启动一个新线程。检查标记.
 sysmon函数是Go runtime启动时创建的，负责监控所有goroutine的状态，判断是否需要GC，进行netpoll等操作。sysmon函数中会调用retake函数进行抢占式调度
 1.14前不具备抢占死循环的gr. 比如 go func(){ for{} }.
`
